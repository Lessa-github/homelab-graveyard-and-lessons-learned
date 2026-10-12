# Case 04: Wazuh SIEM Cluster (6 GB RAM) vs. Velociraptor VQL (67 MB RAM)

Conventional homelab tutorials recommend deploying full enterprise Wazuh clusters with OpenSearch indexers and Kibana/Wazuh dashboards.

On a physical 32 GB host where RAM must sustain 15+ concurrent production services and sovereign AI workflows, dedicating ~20% of physical capacity to Java Virtual Machine (JVM) heaps represented poor SRE judgment.

### The Winning Alternative: Velociraptor
* **Single Statically Compiled Go Binary:** 40 MB executable.
* **Minimal Resource Footprint:** Operates at exactly **67 MB resident physical RAM**.
* **Superior Forensic Depth:** Real-time in-memory digital forensics and threat hunting powered by declarative VQL.
