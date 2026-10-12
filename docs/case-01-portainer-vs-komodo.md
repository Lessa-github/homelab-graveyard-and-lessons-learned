# Case 01: Decommissioning Portainer in Favor of Komodo Orchestrator

## Architectural Liabilities of Portainer
* **Memory Bloat:** Portainer Server and its agents consumed high idle resident memory relative to actual container orchestration workloads.
* **Imperative ClickOps Model:** Encouraged unversioned ad-hoc modifications directly inside the web UI, generating configuration drift and breaking Infrastructure as Code (IaC) guarantees.

## The Engineering Solution: Komodo Orchestrator
* **Rust Periphery Agents:** Each node executes an ultra-lightweight compiled daemon consuming under 18 MB of RAM.
* **Declarative Native GitOps:** Deployment stacks are declared in Git-versioned YAML manifests, guaranteeing deterministic state and atomic rollbacks.
