# ⚰️ Caso 01: Por que Aposentamos o Portainer em Favor do Komodo

Durante a fase inicial do laboratório, utilizamos o **Portainer Business Edition (CT 109)** para gerenciar stacks de contêineres Docker. 

Apesar de ser uma ferramenta consagrada no mercado, sua operação em escala de alta densidade no Proxmox VE revelou limitações estruturais:

---

## 🔍 O Problema Técnico do Portainer

1. **Footprint Excessivo de Agentes:** Cada agente Portainer consumia de 80 a 120 MB de RAM apenas para responder heartbeats de API, além de manter conexões gRPC pesadas e persistentes.
2. **GitOps Frágil:** A sincronização de repositórios Git no Portainer exigia webhooks externos ou polling periódico ineficiente, com histórico de deploys concorrentes que quebravam o estado desejado.
3. **Dependência de UI:** A interface web encorajava modificações manuais fora do código-fonte (*clickOps*), contrariando as boas práticas de infraestrutura declarativa.

---

## 🚀 A Solução: Komodo Orchestrator

Migramos o ecossistema para o **Komodo Orchestrator**:
* **Periphery Agent em Rust:** Consumo inferior a **18 MB de RAM** por nó.
* **GitOps Nativo:** Declaração de stacks em YAML versionadas no Git com sincronização atômica.
* **Zero Telemetria Externa:** O Komodo não envia dados analíticos para nuvens proprietárias.
