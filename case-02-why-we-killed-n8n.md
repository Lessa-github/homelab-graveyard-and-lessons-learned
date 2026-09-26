# Caso 02: O Assassinato do N8N — A Matemática da Memória Node.js

## O Sintoma:
O container do N8N rodando em Node.js com SQLite atingia picos de **1.5 GB a 2.0 GB de RAM** mesmo quando nenhum webhook estava sendo processado ativamente.

## A Decisão:
Descartamos a interface visual de nós para automações críticas do laboratório e escrevemos **scripts modulares em Python e servidores MCP**.

| Métrica | N8N (Node.js) | Scripts Python + FastMCP | Ganho |
| :--- | :--- | :--- | :--- |
| **Footprint em Repouso** | 1.480 MB | **28 MB** | **-98.1% de RAM** |
| **Inicialização** | ~25 segundos | **<0.2 segundos** | **125x mais rápido** |
| **Rastreabilidade** | JSON opaco no banco | Código Python limpo no Git | 100% Auditável |
