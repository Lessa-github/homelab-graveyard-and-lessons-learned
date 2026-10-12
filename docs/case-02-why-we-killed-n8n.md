# ⚰️ Caso 02: Por que Matamos o n8n

O **n8n** é uma ferramenta popular de automação baseada em nós e interface visual para conectar APIs.

No entanto, em um laboratório com limite físico de 32 GB de RAM onde cada megabyte precisa justificar sua existência, o n8n provou ser um dos maiores desperdícios de recursos do ambiente.

---

## 🔍 O Diagnóstico de Memória

* **Overhead da V8 Engine (Node.js):** O processo base do n8n inicia consumindo ~450 MB de RAM.
* **Vazamento Progressivo de Memória:** Ao executar workflows rotineiros (como alertas a cada 5 minutos), a alocação de memória no container CT 115 crescia progressivamente para **mais de 1.500 MB (1.5 GB)** devido à retenção de instâncias de execução e buffers na engine V8.
* **Bloqueio de Event Loop:** Tarefas síncronas pesadas em nós customizados de JavaScript congelavam temporariamente a interface e atrasavam a execução de outros gatilhos.

---

## 🚀 A Solução Adotada

Substituímos o monólito n8n por:
1. **Daemons Python Modulares:** Scripts assíncronos (`asyncio`) consumindo **menos de 30 MB de RAM**.
2. **Servidores MCP (Model Context Protocol):** Wrappers de ferramentas executados sob demanda pelo agente de IA Hermes, com consumo de memória de **zero em repouso**.

**Resultado:** Liberação imediata de **1.450 MB de RAM física** no host Proxmox VE.
