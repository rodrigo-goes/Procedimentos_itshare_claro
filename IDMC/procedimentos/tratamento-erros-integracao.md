# Tratamento de Erros de Integração

- **Responsável:** Equipe Middleware Itshare
- **Última atualização:** 2026-10-27
- **Ambiente:** DEV / HML / PRD

## Objetivo

Padronizar a triagem e as ações para jobs/tarefas IDMC com status *Failed* ou *Warning*.

## Pré-requisitos

- Acesso ao console IDMC (Monitor).
- Conhecimento do fluxo afetado (origem, destino, janela de execução).

## Passo a passo

1. **Identificar o job:** nome da tarefa, ID do job, horário, agente e mensagem de erro (Monitor > My Jobs).
2. **Verificar o agente:** confirmar se está ativo ([monitoramento](monitoramento-secure-agent.md)).
3. **Analisar o log:** conforme [checagem de logs](checagem-de-logs.md).
4. **Classificar o erro:**

| Categoria | Exemplos | Ação inicial |
|-----------|----------|--------------|
| Conectividade | Timeout, connection refused, host inalcançável | Validar rede/firewall e testar a conexão em Administrator > Connections |
| Autenticação | Login failed, senha expirada | Solicitar atualização da credencial ao responsável; não registrar a senha em documentos |
| Dados | Rejeição, violação de constraint, tipo inválido | Identificar registros rejeitados e acionar dono do dado/sistema de origem |
| Recursos | Falta de memória/disco, timeout de sessão | Verificar host do agente; avaliar reprocessamento fora de pico |
| Configuração | Mapeamento/parâmetro inválido, objeto inexistente | Revisar tarefa, parâmetros e versão publicada |

5. **Reprocessar:** após corrigir a causa, reexecutar a tarefa (**Run**) ou aguardar o próximo agendamento, conforme impacto de negócio. Em PRD, confirmar se há risco de duplicidade antes de reexecutar.
6. **Registrar:** anotar causa, ação e resultado na demanda, anexando evidências.

## Validação

- Job concluído com status *Success* e volumes de registros coerentes.
- Destino conferido por amostragem, quando aplicável.

## Escalonamento

- Erro recorrente, impacto em PRD ou causa fora do alcance da equipe: acionar o responsável do sistema envolvido e/ou abrir caso no suporte Informatica com logs e ID do job.

## Referências

- [Monitoramento do Secure Agent](monitoramento-secure-agent.md)
- [Checagem de logs](checagem-de-logs.md)
