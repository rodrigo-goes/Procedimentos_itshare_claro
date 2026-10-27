# Deploy IDMC – NETSMS Faturadores (Reforma Tributária 27)

- **Change/evidência:** 93480 – [evidencia_93480.docx](../evidencias/93480/evidencia_93480.docx)
- **Projeto IDMC:** `di-202506-sinc-nfcom-faturadores-netsms` (origem `...-netsms-rt27`)
- **Org:** Claro HMG-Sandbox
- **Executado em:** 21/10/2026 (usuário `rodrigo.goes.hmg`)
- **Última atualização:** 2026-10-27

## Objetivo

Promover para o projeto `di-202506-sinc-nfcom-faturadores-netsms` as alterações da RT27 (mappings de NETSMS e hierarchical schema SOVOS) e atualizar os arquivos de apoio (query model, default de cabeçalho/item e arquivos de parâmetro) no servidor de Linux do IDMC.

## Pré-requisitos

- Pacote exportado `di-202506-sinc-nfcom-faturadores-netsms-<timestamp>` (export concluído em 21/10/2026 13:26).
- Acesso IDMC (Import/Export) e acesso SFTP (WinSCP) ao servidor do Secure Agent como `infausr` (host `brux2577`).
- Arquivos da change: `query_model_item.txt` e `default_item.txt` (versões novas), demais `query_model_*.txt` e `default_*.txt` inalterados.
- Manual da change aberto para conferir o *Target Project*.

## Passo a passo

### 1. Import dos assets no IDMC

Seguir o runbook base [Export/Import de assets](export-import-assets-idmc.md) com estes valores:

| Campo | Valor |
|-------|-------|
| Job Name | `di-202506-sinc-nfcom-faturadores-netsms-20261021` |
| Overwrite | marcado (exceto conexões e runtime) |
| Source Project | `di-202506-sinc-nfcom-faturadores-netsms-rt27` |
| Target Project | `di-202506-sinc-nfcom-faturadores-netsms` |
| Conexão 1 | `CN_ID202506_ff_nfcom_netsms_STAGE` → mesma (Default) |
| Conexão 2 | `CN_ID202506_ff_nfcom_netsms_TARGET` → mesma (Default) |

Assets (4 de 4 selecionados):

| Asset | Tipo | Resultado esperado |
|-------|------|--------------------|
| `di-202506-m-netsms-en…` | Mapping | Overwrite existing object |
| `di-202506-m-netsms-en…` | Mapping | Create object |
| `di-202506-m-netsms-ge…` (extração das notas, preparação…) | Mapping (1 dependência) | Overwrite existing object |
| `di-202506-hs-sovos-env…` | Hierarchical Schema | Create object |

Executar **Test** (*Test Successful*) e depois **Import**.

### 2. Arquivos no servidor (`brux2577`, usuário `infausr`)

Base: `/app/infa_shared/Projects/di-202506-sinc-nfcom-faturadores-netsms/`

1. **Backup:** antes de substituir, copiar o arquivo atual para `script/bkp/` com sufixo `_<change>_<DDMMAAAA>` (padrão do ambiente; confirmar no manual).
2. **`script/`:** enviar o `query_model_item.txt` novo (6 KB). Demais arquivos (`query_model_cabecalho/contribuinte/endereco/imposto/proc_jur/terminal/xml.txt`, `gera_param_file_NETSMS.sh`) permanecem.
3. **`stage/`:** enviar o `default_item.txt` novo (3 KB). Os `default_*.txt` ficam com permissão **0775**, owner `infausr` e group `infausr`; os `ISP_CICLO_*`/`CTV_CICLO_*` são gerados e permanecem `rw-r-----`.
4. **`parameter/`:** os arquivos `<OPERADORA>_CICLO_<n>.param` (ABC, BHZ, BRA, CTV, ISP, SOC, SPO…, ciclos 0, 5, 8, 10, 15, 20, 25) foram regenerados em 21/10/2026 por volta de 11:57–11:58, ~20 KB cada, owner `infausr`, `rwxrwxr-x`. A evidência indica a geração via `script/gera_param_file_NETSMS.sh`; confirmar no manual da change o comando e os argumentos. `mongoDB.properties` não é alterado.
5. Conferir owner e permissões (`rwxrwxr-x` / 0775) em cada diretório alterado, via *Properties* do WinSCP.

## Validação

- *My Import/Export Logs > Import*: job `di-202506-sinc-nfcom-faturadores-netsms-20261021` com **Import completed successfully**.
- `query_model_item.txt` e `default_item.txt` com data/hora e tamanho novos; demais arquivos inalterados.
- Arquivos `.param` com data/hora da regeneração e owner `infausr`.
- Prints anexados ao [documento de evidência](../evidencias/93480/evidencia_93480.docx).

## Rollback / Escalonamento

- Restaurar `query_model_item.txt` e `default_item.txt` a partir de `bkp/` e reimportar o pacote anterior.
- Dúvida sobre target, conexão ou parâmetros: acionar o desenvolvedor responsável pela change antes de importar.

## Observações da evidência

- Os prints mostram o import dentro da org `Claro HMG-Sandbox` (homologação). Para outro ambiente, repetir a conferência de org, conexões e servidor.

## Referências

- [Export/Import de assets](export-import-assets-idmc.md)
- [Tratamento de erros de integração](tratamento-erros-integracao.md)
