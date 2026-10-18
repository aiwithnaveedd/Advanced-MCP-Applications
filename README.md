# Advanced MCP Applications with Streamable HTTP, Roots, and Sampling

A production-ready implementation of the **Model Context Protocol (MCP)** using Streamable HTTP transport for remote server connectivity, filesystem roots for enterprise security boundaries, and LLM-driven agentic host integration.

This project demonstrates an object-oriented, reusable client-server architecture using **FastMCP**, **LangChain/OpenAI**, and **Gradio**.

---

## 🚀 Key Architectural Features

- **🌐 Streamable HTTP Transport:** Enables remote client-server connectivity over HTTP (`/mcp` endpoint), replacing legacy local STDIO subprocess setups for scalable microservices.
- **🔒 Filesystem Roots Security:** Implemented security boundaries (`is_within_roots`) that prevent directory traversal attacks (e.g., `../../../etc/passwd`) and enforce isolation to an authorized workspace directory.
- **🧠 Synthetic Tools Bridge for LLMs:** Converts native MCP primitives—**Tools**, **Resources**, and **Prompts**—into OpenAI Function-Calling tools, allowing an LLM agent to dynamically list and consume resources or prompts during conversations[cite: 2].
- **🔄 Server-Initiated Sampling Concept:** Demonstrates the `sampling/createMessage` protocol flow where an MCP server requests LLM completions back from the client with human-in-the-loop approval[cite: 2].
- **🧱 Base & Derived Client Architecture:** A decoupled protocol base class (`MCPHTTPClient`)[cite: 2] extended by both a GUI inspection tool (`MCPHTTPClientApp`)[cite: 2] and an AI Assistant Host (`MCPHTTPHostApp`)[cite: 2].

---

## 📂 Repository Structure

```text
mcp_advanced_lab/
├── mcp_http_server.py       # FastMCP HTTP Server exposing tools, resources, and prompts
├── mcp_http_client_base.py   # Pure async protocol client handling Streamable HTTP connections
├── mcp_http_client_app.py   # Gradio-based GUI inspection client for manual testing
├── mcp_http_host_app.py     # AI Host client integrating OpenAI GPT-4o-mini with MCP tools
└── workspace/               # Isolated filesystem roots directory for secure operations

🛠️ Installation & Environment Setup
1. Prerequisites
Python: Version 3.11

[cite: 2]

2. Virtual Environment Setup
Bash
python3.11 -m venv mcp_advanced_env
source mcp_advanced_env/bin/activate
3. Install Dependencies
Bash
pip install mcp==1.16.0 fastmcp==2.12.5 httpx==0.28.1 uvicorn==0.38.0 gradio==5.49.1 openai==2.6.1
🏃 Running the Application
Step 1: Start the Remote HTTP MCP Server
Initialize the FastMCP HTTP server listening on http://127.0.0.1:8000:

Bash
python mcp_http_server.py
Step 2: Option A — Launch the GUI Client App
Run the manual inspection GUI on port 7861:

Bash
python mcp_http_client_app.py [http://127.0.0.1:8000](http://127.0.0.1:8000) workspace
Step 3: Option B — Launch the AI Host Application
Run the LLM-powered Chat Assistant on port 7862:

Bash
python mcp_http_host_app.py [http://127.0.0.1:8000](http://127.0.0.1:8000) workspace

📄 License
This repository is distributed under the MIT License. See LICENSE for details.
