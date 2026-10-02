# Caso 03: Auditoria Estática de Código do Asuri/Azuri

Ao analisar o repositório open-source do Asuri antes de integrá-lo ao pipeline, nossa auditoria estática identificou:
1. Dependências não pinadas com vulnerabilidades críticas conhecidas no ecossistema npm.
2. Falta de sanitização adequada em parâmetros de execução de comandos do sistema operacional.
3. Tratamento de permissões que exigia privilégios de root desnecessários dentro do container.

**Veredito:** O software foi desqualificado e banido do ambiente de produção.
