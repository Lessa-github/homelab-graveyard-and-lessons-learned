# ⚰️ Homelab Graveyard & Lessons Learned

[![Documentation](https://img.shields.io/badge/Docs-Docsify_Live-06b6d4?style=for-the-badge&logo=googledocs&logoColor=white)](https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/)
[![Philosophy](https://img.shields.io/badge/Engineering-Frugal_SRE-orange?style=for-the-badge)](https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/)
[![Culture](https://img.shields.io/badge/Post--Mortems-Honest_Engineering-10b981?style=for-the-badge)](https://github.com/Lessa-github/homelab-graveyard-and-lessons-learned)
[![Status](https://img.shields.io/badge/Decommissioned-4_Major_Stacks-red?style=for-the-badge)](https://lessa-github.github.io/gabriel-portfolio/)

Repository dedicated to **technical honesty and pragmatic Site Reliability Engineering (SRE)**.

In technology, tutorials often teach how to *install* platforms, but rarely analyze the **hidden maintenance cost, memory bloat, and structural vulnerabilities** that these tools introduce to production environments.

This repository compiles the empirical benchmarks, memory profiling sessions, and security audits that justified the **permanent decommissioning and removal** of popular software stacks from my homelab.

---

## 🧭 The Frugal SRE Manifesto

1. **Benchmarking Over Hype:** Any tool claiming "ease of use" that consumes over 1 GB of idle RAM without processing active workloads is a technical liability.
2. **Attack Surface Minimization:** Fewer Node.js or Java runtime dependencies mean fewer unpatched packages and lower exposure to supply chain vulnerabilities.
3. **Declarative GitOps Over Heavy UIs:** Bulky web dashboards encourage unversioned manual changes (*ClickOps*); lean Rust or Go agents driven by Git manifests deliver reproducibility.

---

## 📂 Decommissioned Software Case Studies

```
┌────────────────────────────────────────────────────────────────────────┐
│             DECOMMISSIONED SOFTWARE CASE STUDIES MATRIX                │
├─────────┬──────────────────────┬───────────────────────┬───────────────┤
│ Case    │ Retired Platform     │ Modern Replacement    │ SRE Advantage │
├─────────┼──────────────────────┼───────────────────────┼───────────────┤
│ Case 01 │ Portainer BE         │ Komodo Orchestrator   │ Rust GitOps   │
│ Case 02 │ n8n Workflow Monolith│ Hermes Agent + MCP    │ -1.5 GB RAM   │
│ Case 03 │ Asuri / Azuri        │ Static Audit Disqual. │ Zero Backdoor │
│ Case 04 │ Wazuh SIEM Cluster   │ Velociraptor VQL      │ 67 MB RAM     │
└─────────┴──────────────────────┴───────────────────────┴───────────────┘
```

* **[Case 01: Why We Decommissioned Portainer](https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/#/case-01-decommissioning-portainer-for-komodo):** How migrating to Komodo delivered real GitOps, lower agent latency, and slashed memory overhead.
* **[Case 02: Why We Killed n8n](https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/#/case-02-why-we-killed-n8n--15-gb-ram):** Memory profiling of Node.js processes leaking >1.5 GB of RAM for simple automated webhooks now running in 30 MB via Python and MCP.
* **[Case 03: Asuri Source Code Security Audit](https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/#/case-03-asuri-source-code-security-audit):** How rigorous static application security testing (SAST) intercepted critical command injection vulnerabilities before production deployment.
* **[Case 04: Wazuh Cluster vs Velociraptor](https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/#/case-04-wazuh-cluster-vs-velociraptor-vql):** The mathematics of replacing a 6 GB Elasticsearch cluster with a 67 MB native Go binary for DFIR without sacrificing forensic fidelity.

---

## 🌐 Live Technical Documentation

Explore the complete single-page interactive whitepaper with smooth section scrolling:

👉 **[https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/](https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/)**
