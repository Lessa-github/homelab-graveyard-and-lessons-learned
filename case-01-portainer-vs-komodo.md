# Caso 01: Por que Aposentamos o Portainer em Favor do Komodo

## O Problema do Portainer
* **Consumo de Memória:** O Portainer Server mantinha um footprint elevado para o que oferecia.
* **Modelo Imperativo:** Incentiva a alteração manual de containers via interface gráfica ("clicar para mudar portas"), gerando drift de configuração e quebrando o princípio de infraestrutura como código (IaC).

## A Solução com Komodo Orchestrator
* **Agentes Periphery em Rust:** Cada nó roda um daemon ultraleve em Rust consumindo menos de 15 MB de RAM.
* **GitOps Nativo:** Mudanças são declaradas em arquivos de stack versionados, permitindo rollback imediato.
