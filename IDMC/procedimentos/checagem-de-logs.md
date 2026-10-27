# Checagem de Logs

- **Responsável:** Equipe Middleware Itshare
- **Última atualização:** 2026-10-27
- **Ambiente:** DEV / HML / PRD

## Objetivo

Consultar logs de execução de jobs e do Secure Agent para diagnosticar falhas e comportamentos inesperados.

## Pré-requisitos

- Acesso ao console IDMC (Monitor / Administrator).
- Acesso ao servidor do agente para logs locais.

## Passo a passo

### 1. Logs de jobs (console)

1. Acessar **Monitor > My Jobs** (ou **All Jobs**).
2. Filtrar por nome da tarefa, status (*Failed*, *Warning*) e período.
3. Abrir o job e consultar o resumo (linhas lidas/gravadas/rejeitadas, mensagem de erro).
4. Usar **Download Session Log** / **View Log** para o log detalhado.

### 2. Logs do Secure Agent (servidor)

Caminhos relativos ao diretório de instalação (`<INSTALL_DIR>`):

| Log | Caminho típico |
|-----|----------------|
| Agente (core) | `apps/agentcore/logs/` |
| Data Integration Server | `apps/Data_Integration_Server/logs/` |
| Logs de sessão | `apps/Data_Integration_Server/logs/` e `.../data/` |

> Os caminhos podem variar conforme versão e instalação; confirmar no ambiente.

### 3. Boas práticas de análise

- Começar pela primeira mensagem de erro (não pela última) no log.
- Registrar data/hora, nome da tarefa, ID do job e agente utilizado.
- Salvar o log relevante como evidência (sem dados sensíveis) junto à demanda.

## Validação

- Causa raiz identificada ou evidências coletadas para escalonamento.

## Escalonamento

- Sem causa identificada: seguir para [tratamento de erros de integração](tratamento-erros-integracao.md) e, se necessário, abrir caso no suporte Informatica anexando os logs.

## Referências

- [Monitoramento do Secure Agent](monitoramento-secure-agent.md)
