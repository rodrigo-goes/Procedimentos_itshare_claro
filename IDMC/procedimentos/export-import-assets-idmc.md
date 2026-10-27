# Export/Import de Assets no IDMC (Data Integration)

- **Responsável:** Equipe Middleware Itshare
- **Última atualização:** 2026-10-27
- **Ambiente:** Org `Claro HMG-Sandbox` (evidências 93480 e 93639)
- **Base:** [93480](../evidencias/93480/evidencia_93480.docx) e [93639](../evidencias/93639/evidencia_93639.docx)

Runbook base. Os procedimentos específicos de cada change o referenciam:
[93480 – NETSMS Faturadores](deploy-idmc-netsms-faturadores-rt27.md) e [93639 – Combo Multi Mobile](deploy-idmc-combomulti-mobile-netsms.md).

## Objetivo

Promover assets (mappings, hierarchical schemas etc.) de um projeto IDMC exportado para o projeto de destino, de forma testada e auditável.

## Pré-requisitos

- Acesso à org IDMC (Data Integration) com permissão de Import/Export.
- Pacote exportado (`.zip`) conforme a change, com nome no padrão `<projeto>-<timestamp>`.
- Manual anexo à change aberto, para conferir **Target Project**, conexões e runtime environment.
- Local para salvar as evidências (documento Word, um por change).

## Passo a passo

1. **Export** (se o pacote ainda não existe): Explore > projeto > *Export*. Confirmar em *My Import/Export Logs > Export* o status *Export completed successfully* e anotar o *Instance Name*.
2. Abrir **My Import/Export Logs** e iniciar o **Import Assets** (`.../diUI/products/integrationDesign/main/import`).
3. **Select Import File:** escolher o `.zip` do pacote.
4. **Specify Import Job Details:**
   - *Job Name*: `<nome-do-projeto>-<AAAAMMDD>` (data de execução).
   - Marcar *Overwrite existing assets, excluding connections and runtime environments*.
5. **Select Assets:** conferir a lista (nome, tipo, dependências). Status esperado: *Overwrite existing object* para o que já existe e *Create object* para o que é novo.
6. **Review Locations:** ajustar o **Target Project** exatamente como no manual da change (o *Source Project* costuma terminar em `-rt27` ou `_rt`; o target **não** leva esse sufixo).
7. **Review Connections:** manter o mapeamento *Default* salvo quando o manual indicar outra conexão.
8. **Review Runtime Environments** (quando exibido): selecionar o runtime indicado no manual (ex.: `Claro ICS`).
9. Clicar em **Test** e aguardar *Test Successful*. Não importar se o teste falhar.
10. Clicar em **Import**. Deve aparecer a mensagem *Importing N assets. Check `<job>` for import completion*.
11. Capturar prints de cada etapa (tela de seleção de assets, locations/connections, *Test Successful*, mensagem de importação).

## Validação

- *My Import/Export Logs > Import*: job com status **Import completed successfully**, usuário e horário corretos.
- Quantidade de assets importados igual à selecionada.
- Prints anexados ao documento de evidência da change.

## Rollback / Escalonamento

- Em caso de falha no *Test* ou no *Import*: não repetir às cegas; ler a mensagem do job, conferir target/conexões e acionar o responsável pela change.
- Rollback: reimportar o pacote da versão anterior (exportar a versão atual **antes** de sobrescrever, quando a change permitir).

## Referências

- [Checagem de logs](checagem-de-logs.md)
- [Tratamento de erros de integração](tratamento-erros-integracao.md)
