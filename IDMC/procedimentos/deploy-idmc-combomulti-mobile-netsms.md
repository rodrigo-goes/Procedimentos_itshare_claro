# Deploy IDMC – Combo Multi Mobile NETSMS (Reforma Tributária Residencial)

- **Change/evidência:** 93639 – [evidencia_93639.docx](../evidencias/93639/evidencia_93639.docx)
- **Projeto IDMC:** `di-202509-sinc-nfcom-combomulti-mobile-netsms` (origem `...-netsms_rt`)
- **Org:** Claro HMG-Sandbox
- **Executado em:** 27/10/2026 (usuário `rodrigo.goes.hmg`)
- **Última atualização:** 2026-10-27

## Objetivo

Importar o pacote do projeto Combo Multi Mobile NETSMS (equipe Residencial) para o projeto de destino, usando o target definido no manual.

## Atenção (ponto crítico)

A change vem escrita como "Reforma Tributária Residencial", e o projeto de origem termina em `_rt`. O **Target Project correto não leva o `rt` no final** e deve seguir exatamente o manual:

```
di-202509-sinc-nfcom-combomulti-mobile-netsms
```

## Pré-requisitos

- Pacote exportado `di-202509-sinc-nfcom-combomulti-mobile-netsms-<timestamp>` (export concluído em 27/10/2026 11:20).
- Acesso IDMC (Import/Export) e manual da change com target, conexões e runtime.

## Passo a passo

Seguir o runbook base [Export/Import de assets](export-import-assets-idmc.md) com estes valores:

| Campo | Origem | Destino |
|-------|--------|---------|
| Project | `di-202509-sinc-nfcom-combomulti-mobile-netsms_rt` | `di-202509-sinc-nfcom-combomulti-mobile-netsms` |
| Conexão 1 | `CN_ID202509_ora_nfcom_MOBILE` | `CN_ID202509_ora_nfcom_MOBILE` (Default) |
| Conexão 2 | `CN_ora_NETSMS_oci6isp_combomulti` | `CN_ora_NETSMS_oci7isp_combomulti` (**alterada manualmente**) |
| Runtime Environment | `brux1780.claro.com.br` | `Claro ICS` |

1. Importar o `.zip` e executar **Test** (*Test Successful*).
2. Alterar a *Target Connection 2* para `oci7isp` e o runtime para `Claro ICS`, conforme o manual.
3. Executar **Import**.

## Validação

- *My Import/Export Logs > Import*: job `di-202509-sinc-nfcom-combomulti-mobile-netsms_20261026` com **Import completed successfully** (27/10/2026 11:31).
- Prints anexados ao [documento de evidência](../evidencias/93639/evidencia_93639.docx).

## Observações da evidência

- O nome do job usa `_20261026`, mas a execução ocorreu em 27/10/2026. Usar a data de execução no nome do job (ver runbook base).
- A troca `oci6` → `oci7` foi manual; confirmar no manual da change antes de repetir em outro ambiente.

## Rollback / Escalonamento

- Reimportar o pacote anterior do projeto. Divergência de target/conexão: acionar o desenvolvedor antes de importar.

## Referências

- [Export/Import de assets](export-import-assets-idmc.md)
