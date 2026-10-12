# ⚰️ Caso 03: Auditoria Estática de Código do Asuri / Azuri

Antes de permitir a execução de qualquer ferramenta open-source em nosso ambiente de produção, aplicamos uma diretriz rigorosa de **AppSec e Análise Estática de Segurança (SAST)**.

O caso do projeto **Asuri (ou Azuri)** é um exemplo prático de como essa auditoria salvou o laboratório de uma potencial quebra de segurança.

---

## 🔍 Vulnerabilidades Críticas Identificadas no Código-Fonte

Ao inspecionar diretamente o código-fonte do repositório antes da instalação no Proxmox VE:

1. **Injeção de Comandos Não Sanitizada:** Entrada de usuário em campos de formulário era concatenada diretamente em chamadas de sistema `os.system()` e `subprocess.Popen(shell=True)`.
2. **Exposição de Credenciais em Texto Claro:** Tokens de autenticação e credenciais de banco de dados eram gravados em arquivos de log sem qualquer máscara ou filtro.
3. **Dependências Vulneráveis Desatualizadas:** Pacotes Python obsoletos com CVEs públicas ativas de execução remota de código (RCE).

---

## 🛑 Decisão de Engenharia: Desqualificação Imediata

A ferramenta foi sumariamente **desqualificada para deploy no Homelab**. 

Essa decisão comprova que **adotar software open-source exige due diligence**: nem todo projeto popular no GitHub possui qualidade de código ou segurança aceitável para um ambiente Zero-Trust.
