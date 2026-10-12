# Case 02: Why We Killed n8n — The Mathematics of Node.js Runtime Bloat

## The Diagnostic Symptom:
The monolithic n8n container executing on the Node.js V8 engine with SQLite crept to persistent peaks of **1.5 GB to 2.0 GB of resident RAM**, even during prolonged periods without active webhook payloads.

## The Engineering Decision:
We eliminated visual drag-and-drop workflow graphs for critical homelab automations, replacing them with **lean Python async daemons and lightweight Model Context Protocol (MCP) servers**.

| Architectural Metric | n8n Monolith (Node.js) | Python Async + FastMCP | SRE Gain |
| :--- | :--- | :--- | :--- |
| **Idle Memory Footprint** | 1,480 MB | **28 MB** | **-98.1% Physical RAM** |
| **Daemon Initialization** | ~25 seconds | **<0.2 seconds** | **125x Faster** |
| **Version Auditability** | Opaque database JSON | Clean Git-versioned Python | 100% Code-Reviewable |
