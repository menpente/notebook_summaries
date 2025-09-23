# Briefing Document: AI-Assisted Reddit Scraping Pipeline

## Executive Summary

This project outlines the development of a comprehensive, AI-assisted pipeline designed to scrape content from Reddit, driven by user-defined interests (fuzzy text queries), and store the structured results in a PostgreSQL database managed by Django. The pipeline leverages modern AI tools, including **LangChain** and **Google Gemini**, in conjunction with the specialized scraping services of **Bright Data**, to reliably perform search engine results page (SER) lookups and heavy-duty web scraping. The architecture prioritizes automation, using background task queues (Celery/Django Q Stash) and web hooks for asynchronous data retrieval, making it a resilient and production-ready system. The entire project, known as the **Reddit Content Research Agent**, is open-source.

## Key Project Goals and Outcomes

The core aim of this pipeline is to automate the extraction of community-driven content from Reddit (the world's seventh most visited website) into a relational database.

Key functional outcomes achieved include:

*   **Fuzzy Query to Community Mapping:** The system converts random or vague topics (like "camping and using an RV") into a list of relevant Reddit communities using an AI agent and the SER tool.
*   **Structured Data Extraction:** Utilizing LLMs and Pydantic schemas ensures reliable, structured outputs from the AI and search results, making data storage straightforward.
*   **Asynchronous Scraping:** By triggering external scraping jobs via Bright Data and monitoring their status using web hooks or polling, the system avoids resource blocking and maximizes efficiency.
*   **Automated Tracking:** Django signals and tasks ensure that newly discovered or "trackable" communities are automatically scheduled for content scraping.

## Core Technologies and Components

| Component | Technology Used | Function / Role |
| :--- | :--- | :--- |
| **Primary Backend** | **Python & Django** | Python is the core language. Django manages users, data (ORM), and provides the structure for the comprehensive system. |
| **AI Framework** | **LangChain & LangGraph** | LangChain is the framework for building software on top of LLMs. LangGraph simplifies the complex process of LLM tool calling and agent orchestration. |
| **LLM Provider** | **Google Gemini** | Used for all AI/LLM functionality, including topic extraction and parsing fuzzy text. Supports structured output and tool calling required for the agent model. |
| **Scraping & SER** | **Bright Data** | Provides reliable web scraping services, bypassing issues where websites resist scraping. Used specifically for the SER API (searching Google) and the Web Scraper Library (scraping Reddit content). |
| **Database** | **PostgreSQL & Redis** | PostgreSQL is the preferred production-grade database, managed using Docker Compose. Redis is used for caching and as a broker/backend for task queues. |
| **Task Queues** | **Celery & Django Q Stash** | Used to run background worker processes and scheduled tasks asynchronously. Django Q Stash is a web hook-based alternative to Celery. |
| **Security/DevOps** | **`python-dotenv` & Pre-commit** | Secures API keys and sensitive environment variables. Pre-commit hooks are configured to strip sensitive outputs from Jupyter notebooks before committing code. |
| **Web Hook Handler** | **Cloudflare Tunnel** | Provides a public, secure URL for the local development environment, allowing it to receive notifications (web hooks) from Bright Data when scraping jobs are complete. |

## Pipeline Workflow and Agent Design

The system is built around several AI agents and asynchronous processes to avoid blocking the user.

### Agent Tool Calling

The project utilizes LangGraph to manage AI tool calling. Crucially, LLMs themselves *do not* magically run functions; they suggest the function and arguments based on the query, and the Python code manually executes the tool.

The **hard way** to handle this involves manually using LangChain to get the LLM output (which includes `tool_calls`), executing the functions based on a tool mapping, and then feeding the results back to the LLM for contextual understanding.

The **easy way** uses LangGraph's pre-built agent function (`create_react_agent`) to automatically manage the workflow, state, and decision-making on when to call the tool (like the Bright Data SER tool) and integrate the response.

### Data Flow Overview

1.  **Input & Query Extraction:** A query is submitted (via notebook or `python manage.py query` command). This triggers a background task that uses the LLM (Gemini) to perform **topic extraction** from the input string into a structured Pydantic schema.
2.  **Community Search (SER):** The extracted topics are passed to the **Reddit Agent**. This agent utilizes the **Bright Data SER tool** to perform a localized Google search (e.g., appending "reddit.com" to the search string) to find relevant communities.
3.  **Community Storage:** The extracted Reddit community data (Name, URL, Member Count, Slug) is stored/updated in the Django database. Saving a community instance automatically triggers the scraping process via a database signal.
4.  **Asynchronous Scraping:** The system triggers Bright Data's scraping job by sending the target URL and configuration (e.g., sort by "top," limit 10 posts). This returns a `snapshot ID`.
5.  **Monitoring:** The scraping job status (snapshot progress) is tracked. The primary mechanism for updates is receiving a **Web Hook** notification from Bright Data, or, as a fallback, a scheduled background task continuously checks the snapshot status every few minutes until it transitions to `ready` or `failed`.
6.  **Data Synchronization:** Once the snapshot is ready/downloadable (records > 0), a task downloads the raw results as structured data (JSON format).
7.  **Final Storage:** The results are parsed by a dedicated service that extracts specific fields (post ID, URL, Title, Date Posted, Comments, Upvotes) and stores them as `RedditPost` objects in the Django database (using `update_or_create` to prevent duplicates).

## Development Environment Setup

Key steps for setting up the local environment include:

*   **Dependencies:** Installation of Python packages like `Django`, `LangChain`, `LangGraph`, `psycopg2-binary` (for Postgres), and `python-dotenv`.
*   **Virtual Environment:** Using `Venv` or equivalent (like `UV`) to manage Python dependencies.
*   **Database Management:** Using **Docker Compose** to run isolated PostgreSQL and Redis containers locally, simplifying database management.
*   **Security:** Setting up API keys in a local `.env` file and configuring pre-commit hooks to ensure no sensitive data or outputs are inadvertently pushed to the version control system.
*   **Web Hook Configuration:** If web hooks are required (e.g., for Django Q Stash or real-time Bright Data notifications), a Cloudflare Tunnel is used to expose the local server (e.g., `localhost:8000`) to a public domain. Authorization headers (`Basic` authentication) are used to secure the web hook handler endpoints.
