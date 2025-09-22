https://www.youtube.com/watch?v=rnljvmHorQw

# Briefing Document: Building an MCP Server with Python using Fast MCP

This document provides a high-level overview of the Model Context Protocol (MCP) and details the process of building an MCP server quickly using the Python library **Fast MCP 2.0**.

---

## 1. Model Context Protocol (MCP) Overview

The Model Context Protocol (MCP) is designed to allow external applications (hosts) to interact with localized server processes running on a user's machine.

### Core Architecture
The architecture consists of three main components:
1.  **Host/Client Application:** The application that utilizes the server (e.g., Claude Desktop or Cursor). The client is responsible for *starting* (spawning) the server process.
2.  **Server Process:** The MCP server running locally on the computer, which is what is built using Fast MCP.
3.  **Transport Layer:** The mechanism for communication between the host and the server. This is typically **Standard IO (stdio)** on a local machine.

### Core Capabilities (The Three Aspects of MCP)
An MCP server can expose three main types of functionality to users:

| Capability | Description | Example Functionality |
| :--- | :--- | :--- |
| **Tools** | Functions with defined input schemas, allowing the model to perform specific actions. | `add numbers`, `calculate sum`. |
| **Prompts** | Pre-created, often templated, strings that serve as quick actions or slash commands in the UI. | `code review prompt`, `explain concept prompt`, `debugging assistant prompt`. |
| **Resources** | Mechanisms to expose data from the server's environment or external systems. | Exposing a file, loading data from a cloud bucket, or providing system status information (e.g., server version and datetime). |

---

## 2. Implementation with Fast MCP 2.0

### Why Fast MCP 2.0?
While there is an official Python SDK for MCP, **Fast MCP 2.0 is the actively maintained version** and is recommended for development, as it significantly expands the capabilities of the protocol. The library is noted for its Pythonic, decorator-based interface, drawing inspiration from Fast API.

### Server Construction (Using AI Assistance)
The development process demonstrated involved using an AI assistant (Claude code) to expedite the building process.

1.  **Context and Configuration:** The AI assistant was supplied with documentation context via an `LLMs.txt` file to ensure it used the correct information, specifically for Fast MCP 2.0.
2.  **Project Setup:** The AI handled key setup tasks, including installing dependencies using the rapid virtual environment tool **UV**. UV manages the environment using `pyproject.toml` and requires running `uv sync` to install dependencies.
3.  **Basic Structure:** The server structure involves instantiating the `FastMCP` class and using decorators (`@mcp.tool`, `@mcp.resource`, `@mcp.prompt`) to define the server's capabilities in the main Python file (`main.py`).
4.  **Running Locally:** The server can be run locally using the command `uv run python main.py`. The server logs its startup message, indicating the use of `stdio` transport.

---

## 3. Connecting and Testing the Server

### Client Configuration (Claude Desktop)
To connect the server to a host application like Claude Desktop:
1.  Access the developer configuration file in the client's settings.
2.  Add a server configuration block, including the server name.
3.  Specify the **full path to the UV executable** on the system (`which UV`).
4.  Specify the argument for the current directory, which is the path where the source code is located.
5.  Specify the run command using UV (e.g., `run server py` or `run main py`).
6.  The host application must be restarted to recognize the new configuration.

Once configured, the server will automatically launch (be "spun up") by Claude Desktop when the application starts, confirming its presence by displaying available tools and resources in the client UI.

### Inspection and Debugging
A critical tool for developers is the **MCP Inspector**.

*   **Usage:** By prepending `npx model context protocol inspector` to the server run command, developers can launch the inspector.
*   **Functionality:** The inspector allows developers to connect to the standard IO stream, view logging, list resources and tools, inspect prompt templates, and even run the defined functions directly. This provides detailed debug information crucial for building MCP servers.

---

## 4. Distribution Methods

Developers have options for distributing their finished MCP server to users.

### Option A: GitHub Repository
The simplest method involves placing the code on GitHub and providing instructions:
1.  Users clone the repository.
2.  Users install dependencies locally using UV (`uv sync`).
3.  Users configure their client application (e.g., Claude Desktop) manually to point to the local installation directory and the UV executable.

### Option B: PyPI Package Deployment
For wider distribution, the project can be converted into a proper Python package and deployed to PyPI. This requires substantial restructuring and modification:
1.  **Code Restructuring:** Moving the main server code into a formal source folder structure (e.g., `src/fastmcp_tutorial`) with an `__init__.py` file.
2.  **Metadata Update:** Significantly updating the `pyproject.toml` file to include details like version, description, author names, maintainers, keywords, and license (e.g., MIT).
3.  **Publishing:** Providing detailed instructions for publishing the package to PyPI, allowing users to install it via standard Python package managers (like `pip` or `pipx`).
