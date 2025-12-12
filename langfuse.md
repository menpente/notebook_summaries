# Briefing Document: Langfuse - Open-Source LLM Monitoring

## 1. Executive Summary

**Langfuse** is a highly recommended, **open-source LLM engineering platform** essential for monitoring LLM applications as they transition to production,. It is considered the best platform available due to its effective functionality, quality UI, and fully open-source nature. The self-hosted setup is straightforward, potentially taking **literally five minutes** to get up and running,.

## 2. Core Capabilities and Observability

Langfuse provides comprehensive observability, enabling users to track and analyze interactions with large language models.

| Feature | Description |
| :--- | :--- |
| **Tracking Metrics** | Tracks traces, costs, token usage, and relevant system metrics,. |
| **Model Support** | Provides an overview of interactions with a whole lot of large language models, not only limited to OpenAI. |
| **Trace Management** | Complex chains are tracked as **bundled sessions**. You can inspect individual generation steps, viewing elements like the **system prompt**, the **user prompt**, and the resulting assistance call or final output (e.g., a dictionary or response model),. |
| **Engineering Tools** | Supports prompt management and evaluation functionality (evals). |

## 3. Self-Hosted Setup Guide

The self-hosted instance of Langfuse can be set up quickly using Docker,.

### Prerequisites
To follow the self-hosted guide, you need:
*   **Docker** installed.
*   **Python** installed.
*   An **OpenAI API key**.

### Setup Steps
1.  **Clone the repository** (e.g., the streamlined Langfuse self-hosted repository),.
2.  **Create the `.env` file** based on the `.env.example` file. This step ensures configuration variables are excluded from Version Control systems (like Git),.
3.  Execute **`docker compose up -d`**. This starts the Docker container in detached mode and relies on a **PostgreSQL database** to store data. The database is mounted as a volume to ensure the data is **persistent** when the Docker container is closed or restarted.
4.  Navigate to **`Localhost:3000`** in the browser, sign up, and create a new project.
5.  Retrieve the host URL and generate a new API key. It is critical to **store the secret key immediately**, as it can only be viewed once.

## 4. Integrating Langfuse into LLM Projects

To capture traces and monitor your LLM application, you must integrate the Langfuse client.

1.  **Configure Environment Variables:** Add the saved **secret key, public key, and host** information to the environment file of your LLM project.
2.  **Install and Import:** Install the package using `pip install langfuse`. Import the **`@observe` decorator** and obtain the LLM client (e.g., the OpenAI client) through the Langfuse integration.
3.  **Capture Traces:** Wrap the function that calls the large language model (e.g., OpenAI) with the **`@observe` decorator**. You can optionally pass a **session ID** to the decorator to bundle related calls together.

## 5. Deployment and Security Next Steps

### Deployment
Since the application utilizes Docker and Docker Compose, deployment to various cloud platforms is easy. The official self-host documentation provides platform-specific information for services such as **Railway, GCP, Microsoft Azure, AWS, and Heroku**.

### Security Enhancements
The default sign-in uses email and password. For enhanced security, particularly if deploying to a public URL or adding clients as members, **OAuth** can be enabled. This involves updating the `.env` file to support authentication options such as **GitHub, Google, or Azure**, which will display a "Sign in with GitHub" button on the sign-up page. Documentation provides details on acquiring the necessary credentials for OAuth.
