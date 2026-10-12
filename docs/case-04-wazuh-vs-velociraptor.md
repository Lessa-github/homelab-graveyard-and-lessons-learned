# ⚰️ Caso 04: Wazuh SIEM Cluster vs Velociraptor VQL

O **Wazuh** é um excelente SIEM/XDR corporativo, mas sua arquitetura baseada em **Elasticsearch/OpenSearch e JVM (Java)** impõe uma penalidade de hardware severa.

---

## 🔍 A Análise de Custos de Hardware

Para manter um cluster Wazuh minimamente saudável em produção com ingestão de logs de 12 CTs:
* **Indexer OpenSearch (JVM):** Mínimo de 4.096 MB (4 GB) de RAM apenas para heap alocado.
* **Wazuh Server & Dashboard:** Outros 2.048 MB (2 GB) de RAM.
* **Total Consumido:** **Mais de 6 GB de RAM** (quase 20% da capacidade total de 32 GB do Mini-PC) e gravação contínua em disco NVMe, encurtando a vida útil do SSD via *write endurance exhaustion*.

---

## 🚀 A Alternativa Vencedora: Velociraptor (Go Estático)

Substituímos o cluster de 6 GB pelo **Velociraptor**:
* **Binário Estático em Go:** Servidor consome apenas **67 MB de RAM física**.
* **Sem Indexação Massiva:** Em vez de salvar milhões de linhas de log inofensivas, o analista dispara consultas VQL expressivas para caçar anomalias específicas na memória dos endpoints.
* **Mesma Eficácia Forense:** Capacidade de resposta rápida a incidentes e caça a ameaças preservando **5.933 MB de memória RAM** para outros serviços essenciais.
