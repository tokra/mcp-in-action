# Presentation: MCP (Model Context Protocol) In Action (Unlocking the Power of Model Context Protocol (MCP) in Agentic AI)

### 🌍 Title:

**MCP (Model Context Protocol) In Action (Unlocking the Power of Model Context Protocol (MCP) in Agentic AI)**

## ✈️ Agenda:

1. **The Problem in Agentic AI World**
2. **What is MCP (Model Context Protocol)?**
3. **Why MCP Matters: Key Benefits**
4. **Architecture Overview & Workflow**
5. **What Can MCP Enable?**
6. **Why Does MCP Matter?**
7. **MCP in Action (Live Demo Overview)**
8. **Connecting MCP to Elasticsearch (RAG Use Case)**
9. **Future Outlook + Q&A**

---

## 1. The Problem in Agentic AI World

Current technologies are not easily pluggable into agentic AI — each tool has its own APIs, SDKs, and integration logic, with **no shared standard for interoperability**. Beyond that, these tools also return data and models in non-standardized formats — for example, a SQL database like Db2 requires a dedicated SQL client to access it and doesn't expose its capabilities to the system (e.g., which methods or actions it supports). REST APIs may provide partial self-discovery via Swagger or OpenAPI specs, but this still requires manual parsing and client-side logic. **MCP solves this by enforcing structured interaction and automatic self-discovery between clients and tools.** **MCP overcomes this by bridging these disparate systems under one protocol.**

* Tool use, embeddings, retrieval systems, LLM calls, and context windows are often **loosely coupled** (i.e., tools don't share memory or state across steps, embeddings aren’t reused efficiently, retrieval isn’t aware of evolving context, and LLMs operate in isolated, stateless calls).

✅ **What MCP does do:**

* Standardizes how tools (like a retrieval service) expose their capabilities
* Allows a client (e.g., an agent) to discover what a retrieval tool can do
* Defines how to send structured inputs and receive structured outputs
* Optionally allows state to be passed between tool invocations, *if the client/agent tracks that state*

---

## 2. What is MCP?

> **Model Context Protocol (MCP)** is a lightweight coordination standard for managing shared memory, tools, and execution plans between LLM agents and their environment.

* **MCP is an open, standardized protocol** that acts like **USB‑C for AI** — a universal port that enables **secure, bidirectional communication** between agents and tools, with built-in support for **self-discovery and structured input/output**.
* Anthropic provides reference MCP servers for tools like Google Drive, GitHub, Slack, Postgres, Puppeteer, etc.
* Claude supports MCP **natively**, making it easier to integrate without writing client logic manually.

### 🖥️ Examples of MCP Clients & Integrations

* **Claude Desktop** (full-featured, resources + tools)
* **Claude Code** (developer-focused client)
* **Postman** (used for testing and interacting with MCP server APIs)
* **LangChain** (supports integration with MCP-compliant toolchains)
* **BeeAI Framework** (agentic framework with built-in MCP tool compatibility)
* **Chatbox** (community UI client supporting remote MCP servers)
* **Dolphin‑MCP** (open-source CLI bridging client)
* **ChatMCP** (experimental open-source interface)

Additional known MCP-compatible clients:

* **oterm, Roo Code, RecurseChat, Shortwave, Simtheory** (editor/chat/agent UIs)
* **Slack MCP Client** (messaging interface)
* **Sourcegraph Cody, VS Code, GitHub Copilot, Zed** (dev tool integrations)
* **Tambo, Superinterface, TypingMind, Windsurf Editor, TheiaIDE** (productivity and IDE tools)
* **Warp, Tome, Superjoin, WhatsMCP, Witsy, Zencoder** (various UI and task-based clients)

> ⚠️ Note: Each client may support a different subset of MCP capabilities (e.g. prompts, discovery, or tool use).

**Sources:**

* [Anthropic Engineering Blog](https://www.anthropic.com/news/model-context-protocol)
* [Anthropic Documentation – MCP](https://docs.anthropic.com/en/docs/mcp)
* [modelcontextprotocol.io – Clients List](https://modelcontextprotocol.io/clients)

---

## 3. Why MCP Matters

| Challenge                | Without MCP      | With MCP                                          |
| ------------------------ | ---------------- | ------------------------------------------------- |
| Multi-tool coordination  | Manual & fragile | Seamless protocol-driven execution                |
| Reusability              | Ad-hoc           | Modular components with defined context contracts |
| Debugging & replay       | Difficult        | Full traceability and introspection               |
| Search & RAG integration | Static           | Dynamic queries with embedded context             |
| Model-aware reasoning    | Stateless calls  | Stateful sessions with memory & history           |

---

## 4. Architecture Overview

* Agents or workflows communicate with MCP via `fastmcp` or custom protocol wrappers.
* MCP manages:

  * **Memory** (contextual state across steps)
  * **Tools** (search, embedding, retrieval, actions)
  * **Model interaction** (prompt structuring, execution plan)
* Can be used standalone or in LangChain / LangGraph pipelines.

**Your Setup:**

* Implemented using `fastmcp`
* Integrated with LangChain tools

![MCP Simple Diagram](https://mintcdn.com/mcp/4ZXF1PrDkEaJvXpn/images/mcp-simple-diagram.png?fit=max\&auto=format\&n=4ZXF1PrDkEaJvXpn\&q=85\&s=9337f8096debc55621adcaf8ca563695)

---

## 4.1 How MCP Can Run

MCP-compatible tools and agents can run in various environments depending on how you implement your architecture:

* **HTTP Server** – tools and capabilities are exposed as REST endpoints, typically behind a reverse proxy (common in cloud-native apps)
* **SSE (Server-Sent Events)** – enables streaming output from tools or models back to the client in real time (ideal for chat interfaces or long-running tool actions)
* **STDIO Tool Library** –  MCP tools can also be packaged as CLI processes or subprocesses communicating via stdin/stdout (useful for local agents, scripting, and other environments). This is especially useful when creating an MCP wrapper for your internal technology (e.g., Search API, database, etc.), where you want to expose only a controlled set of tools. Developers or adopters can include such a wrapper library in their app/agent/system by configuring it via environment variables — think of it as an MCP-ready wrapper library published to Artifactory or other internal registries.

These modes can be mixed and matched depending on whether you're deploying in a microservice-based setup, CLI-first agent shell, or hybrid cloud + local dev environment.

---

## 5. What Can MCP Enable?

* Agents can access your Google Calendar and Notion, acting as a more personalized AI assistant.
* Claude Code can generate an entire web app using a Figma design.
* Enterprise chatbots can connect to multiple databases across an organization, empowering users to analyze data using chat.
* AI models can create 3D designs on Blender and print them out using a 3D printer.

---

## 6. Why Does MCP Matter?

Depending on where you sit in the ecosystem, MCP can have a range of benefits:

* **Developers:** MCP reduces development time and complexity when building, or integrating with, an AI application or agent.
* **AI applications or agents:** MCP provides access to an ecosystem of data sources, tools and apps which will enhance capabilities and improve the end-user experience.
* **End-users:** MCP results in more capable AI applications or agents which can access your data and take actions on your behalf when necessary.

---

## 7. MCP in Action (Live Demo Preview)

You will demonstrate:

* Initialization of MCP server or connecting MCP Tools via desktop MCP client (Claude/Postman)
* Tool loading (e.g., ElasticSearch, ...)
* Context evolution over multi-step chain (reasoning can be seen in clients like Claude)

Key visual: **tool + memory + prompt chain coordination**

---

## 8. Connecting MCP to Elasticsearch

Use Case: **RAG (Retrieval-Augmented Generation)**

* Load ElasticSearch MCP tooling via Claude or LangChain tool via MCP
* Perform keyword or vector or hybrid search

**Benefits:**

* Self-updating queries
* Context-aware retrieval
* Easier traceability for audit/debug

---

## 9. Future Outlook + Q&A

* Future: MCP for autonomous agents, planning systems, toolchains
* Open-source potential & community standards
* Interop with OSS agents (e.g., LangGraph, ReAct agents)

---

## Closing Line:

> "MCP is not just a protocol. It's the nervous system for next-gen intelligent agents."

---

## 🎥 Visuals:

* Diagram: MCP node between LLM, tools, memory, and user
* Table: Before/after MCP comparison
* JSON snapshot: Sample MCP context object

---

**Prepared by:** *Tomáš Kramarič*
