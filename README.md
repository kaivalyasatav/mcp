# 📦 mcp – Model Context Protocol

---

## Overview

`mcp` (Model Context Protocol) is a versatile framework that provides **LangChain adapters**, **terminal‑server implementations**, and **Docker‑based deployment** for interacting with Large Language Models (LLMs) using a unified protocol.  The repository contains:

- **Client adapters** – Python packages that expose a simple API for sending prompts and receiving structured responses.
- **Server implementations** – A lightweight terminal server that can be run locally or inside Docker.
- **Docker images** – Ready‑to‑run containers for quick experimentation.
- **Documentation & examples** – Sample scripts and notebooks demonstrating typical workflows.

The goal is to make it straightforward to plug any LLM backend (OpenAI, Anthropic, Gemini, etc.) into a **Model Context Protocol** that standardises request/response handling, streaming, and tool usage.

---

## Folder Structure

```
.
├── clients/                         # Client‑side adapters
│   └── mcp-client/                  # Python package – pip installable
├── servers/                         # Server implementations
│   └── terminal_server/              # Minimal terminal‑server
├── Docker/                          # Docker‑related files
│   └── terminal_server/               # Dockerfile & compose example
├── workspace/                       # Sample data, notebooks, test outputs
├── finalmcp.pdf                     # PDF documentation (generated)
├── .gitignore                       # Excludes virtualenvs, secrets, OS files
└── README.md                        # <‑‑ This file
```

---

## Installation

> **Prerequisites**: Python 3.10+, Git, and optionally Docker.

### 1. Clone the repository

```bash
git clone https://github.com/kaivalyasatav/mcp.git
cd mcp
```

### 2. Set up a Python virtual environment (recommended)

```bash
python -m venv .venv
source .venv/bin/activate   # on macOS / Linux
# .venv\Scripts\activate   # on Windows
```

### 3. Install the client package (editable)

```bash
pip install -e clients/mcp-client
```

### 4. Install the server dependencies

```bash
pip install -r servers/terminal_server/requirements.txt
```

### 5. (Optional) Build the Docker image

```bash
cd Docker/terminal_server
docker build -t mcp-terminal .
```

---

## Quick Start

### Run the terminal server locally

```bash
python servers/terminal_server/main.py
```

The server will start on `http://localhost:8000`.  You can now interact with it via the client library:

```python
from mcp_client import MCPClient

client = MCPClient(base_url="http://localhost:8000")
response = client.chat(prompt="Explain the difference between GPT‑4 and Claude.")
print(response)
```

### Using the Docker container

```bash
docker run -p 8000:8000 mcp-terminal
```

Then use the same client code as above, pointing to `http://localhost:8000`.

---

## Development & Contribution

1. **Branching** – Work on feature branches and submit a Pull Request.
2. **Testing** – Run the test suite with `pytest` from the repository root.
3. **Code style** – The project follows `ruff`/`black` formatting; run `ruff .` and `black .` before committing.
4. **Documentation** – Add or update examples in the `workspace/` folder and keep the PDF (`finalmcp.pdf`) in sync.

---

## License

`mcp` is licensed under the **MIT License** – see the `LICENSE` file for details.

---

## Acknowledgements

- Built on top of **LangChain** for LLM orchestration.
- Inspired by the **Model Context Protocol** research series by Krish Naik.
- Thanks to the open‑source community for tooling like `ruff`, `pytest`, and `Docker`.

---

*Happy hacking! 🚀*
