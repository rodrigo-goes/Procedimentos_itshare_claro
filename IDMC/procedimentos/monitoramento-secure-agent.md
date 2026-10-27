# Monitoramento do Secure Agent

- **Responsável:** Equipe Middleware Itshare
- **Última atualização:** 2026-10-27
- **Ambiente:** DEV / HML / PRD

## Objetivo

Verificar se os Secure Agents estão ativos e com todos os serviços necessários em execução.

## Pré-requisitos

- Acesso ao console IDMC (Administrator) com perfil que permita ver *Runtime Environments*.
- Acesso ao servidor do agente (RDP/SSH), quando for necessário agir no host.

## Passo a passo

### 1. Verificar status no console

1. Acessar **Administrator > Runtime Environments**.
2. Localizar o grupo de agentes e conferir o status de cada agente (*Up and Running* esperado).
3. Abrir o agente e verificar os serviços (Data Integration Server, Process Server, etc.) – todos devem estar *Running*.
4. Anotar agentes em *Inactive*, *Stopped* ou com serviços em erro.

### 2. Verificar no servidor (se o agente estiver inativo)

- **Windows:** abrir `services.msc` e checar o serviço *Informatica Cloud Secure Agent*.
- **Linux:** dentro do diretório de instalação do agente:
  ```bash
  cd <INSTALL_DIR>/apps/agentcore
  ./infaagent status
  ```
- Verificar recursos do host: CPU, memória, disco (principalmente o volume do diretório de instalação e de logs).

### 3. Reiniciar o agente (se necessário)

- **Windows:** reiniciar o serviço pelo `services.msc`.
- **Linux:**
  ```bash
  ./infaagent shutdown
  ./infaagent startup
  ```
- Aguardar alguns minutos e confirmar o status no console.

## Validação

- Agente com status ativo no console e todos os serviços *Running*.
- Jobs agendados voltam a ser executados normalmente.

## Escalonamento

- Se o agente não subir após reinício, ou houver falta de espaço/recursos no host: coletar logs ([checagem de logs](checagem-de-logs.md)) e acionar a equipe de infraestrutura e/ou o suporte Informatica.

## Referências

- [Checagem de logs](checagem-de-logs.md)
- [Tratamento de erros de integração](tratamento-erros-integracao.md)
