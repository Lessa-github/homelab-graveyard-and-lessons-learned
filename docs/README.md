# ⚰️ Homelab Graveyard: O Manifesto da Frugalidade em Engenharia

> **Autor:** Gabriel Santa Rosa Lessa  
> **Linha do Tempo:** 2025 – Presente  
> **Foco:** Honestidade Técnica · Métricas Reais de Hardware · Eliminação de Dívida Técnica

Em engenharia de confiabilidade de sites (SRE), a habilidade mais subestimada não é adicionar ferramentas, mas saber **quando e por que remover ferramentas**.

---

## 🛑 Os 3 Sintomas da Dívida Técnica em Homelabs

1. **Monólitos Ociosos Consumindo Memória:** Frameworks que demandam mais de 1 GB de RAM sem estar processando nenhuma carga de trabalho útil.
2. **Loops de Telemetria:** Agentes de observabilidade que geram tanta sobrecarga de CPU e I/O de disco que desestabilizam as próprias aplicações que deveriam proteger.
3. **Falso Conforto de UIs Web:** Interfaces web bonitas que escondem scripts frágeis, ausência de controle de versão (GitOps) e falhas de segurança na autenticação.

---

## 📊 Navegação pelos Casos de Estudo

* **[Caso 01: Portainer vs Komodo](case-01-portainer-vs-komodo.md)** — Como o Rust e GitOps substituíram um gerenciador com footprint excessivo.
* **[Caso 02: Por que Matamos o n8n](case-02-why-we-killed-n8n.md)** — Como economizamos 1.5 GB de RAM substituindo um monólito Node.js por daemons Python e MCP.
* **[Caso 03: Auditoria do Asuri](case-03-asuri-source-audit.md)** — Como a engenharia reversa de código barrou falhas de injeção antes da produção.
* **[Caso 04: Wazuh vs Velociraptor](case-04-wazuh-vs-velociraptor.md)** — Por que trocar 6 GB de Elasticsearch por 67 MB de Go para resposta a incidentes.
