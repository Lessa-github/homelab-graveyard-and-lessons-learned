# ⚰️ Homelab Graveyard & Lessons Learned: The Frugal SRE Manifesto

> **Author:** Gabriel Santa Rosa Lessa  
> **Timeline:** 2025 – Present (College Studies 2025 - Aug/2026 · Intensive Hands-on Aug/2026 - Present)  
> **Core Focus:** Technical Honesty · Hardware Resource Profiling · Technical Debt Elimination  
> **Culture:** Engineering Post-Mortems & Pragmatic Software Architecture Tradeoffs

---

## 📋 The Frugal SRE Manifesto :id=frugal-manifesto

In Site Reliability Engineering (SRE), the most underappreciated senior competency is not knowing what tools to install, but knowing **when and why to remove tools**.

Too many homelab guides promote heavy enterprise platforms without addressing their **hidden operational costs: memory leaks, JVM heap overhead, complex upgrade paths, and telemetry feedback loops**.

This repository documents the benchmarks, memory profiling sessions, and security audits that led to the **permanent decommissioning and removal of popular software stacks** from my Proxmox VE homelab.

### The 3 Core Tenets of Frugal SRE:
1. **Benchmarking Over Hype:** Any tool claiming "ease of use" that consumes over 1 GB of idle RAM without processing active workloads is a technical liability.
2. **Attack Surface Minimization:** Fewer Node.js or Java runtime dependencies mean fewer unpatched packages and lower exposure to supply chain vulnerabilities.
3. **Declarative GitOps Over Heavy UIs:** Bulky web dashboards encourage unversioned manual changes (*ClickOps*); lean Rust or Go agents driven by Git manifests deliver reproducibility.

---

## 📊 Summary of Decommissioned Stacks :id=summary-matrix

| Case Study | Retired Platform | Modern Replacement | Primary SRE Advantage | Net Resource Impact |
| :---: | :--- | :--- | :--- | :---: |
| **Case 01** | `Portainer Business Edition` | `Komodo Orchestrator` (Periphery) | Declarative Rust GitOps & Atomic Sync | **<18 MB RAM** per agent |
| **Case 02** | `n8n Workflow Monolith` | `Hermes Autonomous Agent + MCP` | Event-driven async Python & on-demand execution | **-1,450 MB RAM** reclaimed |
| **Case 03** | `Asuri / Azuri Scanner` | `Static SAST Code Audit (Disqualified)` | Elimination of arbitrary command injection | **Zero Backdoor Risk** |
| **Case 04** | `Wazuh + OpenSearch SIEM` | `Velociraptor VQL Engine` | Live surgical endpoint queries vs JVM heap bloat | **-5,933 MB RAM** (98.9% less) |

---

## ⚰️ Case 01: Decommissioning Portainer for Komodo :id=case-01-portainer

During early lab iterations, **Portainer Business Edition (CT 109)** was deployed to manage Docker container stacks. While popular, high-density operation exposed architectural bottlenecks:

### Architectural Pain Points with Portainer:
1. **Agent Memory Bloat:** Each Portainer agent consumed 80 to 120 MB of RAM simply maintaining persistent gRPC polling sessions.
2. **Fragile GitOps:** Repository synchronization relied on webhooks or inefficient polling, leading to race conditions during multi-container updates.
3. **ClickOps Drift:** The web GUI encouraged ad-hoc configuration adjustments outside version control.

### The Engineering Solution: Komodo Orchestrator
We migrated container orchestration to **Komodo**:
* **Rust Periphery Agent:** Consumes **under 18 MB of RAM** per node.
* **Declarative GitOps:** Native YAML stacks version-controlled in Git with atomic reconciliation.
* **Zero External Telemetry:** No analytics beacons sent to third-party cloud telemetry services.

---

## ⚰️ Case 02: Why We Killed n8n (-1.5 GB RAM) :id=case-02-n8n

**n8n** is a widespread visual workflow automation platform. In an environment with a finite 32 GB RAM ceiling where every service must justify its presence, n8n proved unviable:

### Memory Profiling Diagnosis:
* **V8 Engine Base Overhead:** Idle baseline started at ~450 MB RAM.
* **Progressive Memory Leaking:** Under routine 5-minute cron triggers (such as Uptime Kuma alert hooks), memory consumption inside container CT 115 crept to **over 1,500 MB (1.5 GB)** due to V8 execution context retention.
* **Event Loop Blocking:** Synchronous JavaScript node processing occasionally locked the event loop, delaying consecutive triggers.

### The Engineering Solution:
Replaced the n8n monolith with:
1. **Asynchronous Python Daemons (`asyncio`):** Consuming **less than 30 MB of RAM**.
2. **Model Context Protocol (MCP) Tools:** Invoked on-demand by the Hermes AI agent, with **zero memory consumption when idle**.

**Net SRE Outcome:** Immediate reclamation of **1,450 MB of physical RAM**.

---

## ⚰️ Case 03: Asuri Source Code Security Audit :id=case-03-asuri

Before allowing any third-party open-source repository into production, we execute strict **AppSec and Static Application Security Testing (SAST)**. The case of the **Asuri (or Azuri)** tool exemplifies why code review precedes deployment:

### Critical Security Vulnerabilities Found:
1. **Unsanitized Command Concatenation:** User input fields were concatenated directly into shell execution routines (`os.system()` and `subprocess.Popen(shell=True)`).
2. **Cleartext Credential Logging:** Database credentials and API authentication tokens were dumped to plaintext log files.
3. **Outdated Vulnerable Dependencies:** Python packages with known high-severity CVEs for Remote Code Execution (RCE).

### Engineering Outcome: Immediate Disqualification
The software was **summarily disqualified** from deployment. This case study demonstrates that open-source popularity does not substitute for defensive source code verification.

---

## ⚰️ Case 04: Wazuh Cluster vs Velociraptor VQL :id=case-04-wazuh

**Wazuh** is a respected enterprise SIEM, but its architecture—built on **OpenSearch/Elasticsearch and the Java Virtual Machine (JVM)**—imposes severe hardware taxation:

### Hardware Cost Analysis:
* **OpenSearch Indexer Heap:** Required at least 4,096 MB (4 GB) of RAM just for JVM heap stability.
* **Wazuh Server & Dashboard:** Added another 2,048 MB (2 GB) of RAM.
* **Total Resource Tax:** **Over 6 GB of RAM** (nearly 20% of total host capacity) with continuous NVMe disk write cycles that rapidly degrade SSD endurance.

### The Winning Alternative: Velociraptor
Replaced the 6 GB cluster with **Velociraptor**:
* **Static Go Binary:** Server runs in an exact **67 MB physical RAM footprint**.
* **On-Demand Memory Querying:** Rather than indexing gigabytes of benign logs, the SOC queries live endpoint state using declarative VQL.
* **Equivalent Forensic Fidelity:** Preserves **5,933 MB of RAM** for core homelab services without sacrificing incident response depth.

---

## 🔗 Connected Portals :id=connected-portals

* 🏛️ **[Homelab Zero-Trust](https://lessa-github.github.io/homelab-zero-trust-infra/)** — Network Topology, Proxmox VE & SRE Hardening.
* 🛡️ **[Cyber DFIR Training Lab](https://lessa-github.github.io/cyber-dfir-training-lab/)** — Digital Forensics, Velociraptor (67MB RAM) & Purple Teaming.
* 🧠 **[Sovereign AI Workspace](https://lessa-github.github.io/sovereign-ai-workspace/)** — Multi-Provider Gateway, Caveman Compression & Private Search.
* 🌐 **[Gabriel Lessa Portfolio](https://lessa-github.github.io/gabriel-portfolio/)** — Cybersecurity Risk Management & Homelab Engineering.

