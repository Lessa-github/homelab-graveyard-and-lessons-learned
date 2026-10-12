# ⚰️ Homelab Graveyard & Lessons Learned

[![Documentation](https://img.shields.io/badge/Docs-Docsify_Live-06b6d4?style=for-the-badge&logo=googledocs&logoColor=white)](https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/)
[![Philosophy](https://img.shields.io/badge/Engineering-Frugal_SRE-orange?style=for-the-badge)](https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/)
[![Culture](https://img.shields.io/badge/Post--Mortems-Honest_Engineering-10b981?style=for-the-badge)](https://github.com/Lessa-github/homelab-graveyard-and-lessons-learned)
[![Status](https://img.shields.io/badge/Decommissioned-4_Major_Stacks-red?style=for-the-badge)](https://lessa-github.github.io/gabriel-portfolio/)

Repositório dedicado à **honestidade técnica e ao pragmatismo em SRE (Site Reliability Engineering)**.

Em tecnologia, a maioria dos tutoriais ensina apenas como *instalar* ferramentas, mas raramente aborda o **custo oculto de manutenção, vazamento de memória e vulnerabilidades estruturais** que essas ferramentas trazem para ambientes reais.

Este repositório reúne os estudos de caso, testes de estresse e auditorias que justificaram o **descarte e a aposentadoria definitiva** de softwares populares no meu Homelab.

---

## 🧭 O Manifesto da Frugalidade em Engenharia

1. **Medir Sempre Supera o Hype:** Qualquer software que reivindica "facilidade de uso" mas consome mais de 1 GB de RAM ocioso é um passivo técnico em ambientes com recursos finitos.
2. **Menos Superfície de Ataque:** Menos dependências em Node.js ou Java rodam menos processos em background e apresentam menor risco de vulnerabilidades na cadeia de suprimentos (*supply chain attacks*).
3. **GitOps Declarativo sobre UIs Pesadas:** Gerenciadores com painéis web pesados adicionam camadas redundantes que podem ser substituídas com elegância por código de infraestrutura declarativo e agentes leves em Rust ou Go.

---

## 📂 Os 4 Casos de Estudo Documentados

```
┌────────────────────────────────────────────────────────────────────────┐
│               RESUMO DOS ESTUDOS DE CASO DE DESCARTE                   │
├─────────┬──────────────────────┬───────────────────────┬───────────────┤
│ Caso    │ Software Descartado  │ Solução Adotada       │ Ganho Técnico │
├─────────┼──────────────────────┼───────────────────────┼───────────────┤
│ Caso 01 │ Portainer BE         │ Komodo Orchestrator   │ Rust GitOps   │
│ Caso 02 │ n8n Workflow Monolit │ Hermes Agent + MCP    │ -1.5 GB RAM   │
│ Caso 03 │ Asuri / Azuri        │ Auditoria Reprovada   │ Zero Backdoor │
│ Caso 04 │ Wazuh SIEM Cluster   │ Velociraptor VQL      │ 67 MB RAM     │
└─────────┴──────────────────────┴───────────────────────┴───────────────┘
```

* **[Caso 01: Por que Aposentamos o Portainer](https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/#/case-01-portainer-vs-komodo):** Como a migração para o Komodo nos deu GitOps real, menor latência de agente e reduziu a pegada de memória.
* **[Caso 02: Por que Matamos o n8n](https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/#/case-02-why-we-killed-n8n):** Análise de consumo de processos Node.js acumulando mais de 1.5 GB de RAM para automações simples que hoje rodam em 30 MB via daemons Python e MCP.
* **[Caso 03: Auditoria Estática de Código do Asuri](https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/#/case-03-asuri-source-audit):** Como uma inspeção reversa rigorosa no repositório GitHub identificou vulnerabilidades graves antes de qualquer deploy em produção.
* **[Caso 04: Wazuh Cluster vs Velociraptor](https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/#/case-04-wazuh-vs-velociraptor):** A matemática de trocar 6 GB de RAM de um cluster Elasticsearch por 67 MB de um binário Go nativo para DFIR com a mesma eficácia forense.

---

## 🌐 Documentação Web Completa (Live Docsify)

👉 **[https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/](https://lessa-github.github.io/homelab-graveyard-and-lessons-learned/)**
