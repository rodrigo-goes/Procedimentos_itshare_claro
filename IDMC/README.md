# IDMC – Informatica Intelligent Data Management Cloud

Documentação operacional da Equipe Middleware Itshare para o ambiente IDMC (Claro).

## Estrutura da pasta

```
IDMC/
├── README.md                          <- este índice
├── evidencias/                        <- evidências originais (.docx) por change
│   ├── 93480/evidencia_93480.docx
│   ├── 93584/evidencia_93584.docx
│   └── 93639/evidencia_93639.docx
└── procedimentos/
    ├── README.md                      <- índice dos procedimentos
    ├── _template-procedimento.md
    ├── (operação) monitoramento-secure-agent.md, checagem-de-logs.md, tratamento-erros-integracao.md
    └── (changes) export-import-assets-idmc.md, deploy-*.md
```

## Procedimentos de mudança (baseados em evidências reais)

| Change | Procedimento | Cenário | Evidência |
|--------|--------------|---------|-----------|
| (base) | [Export/Import de assets](procedimentos/export-import-assets-idmc.md) | Passos comuns de import no IDMC, com Test antes do Import | 93480, 93639 |
| 93480 | [Deploy NETSMS Faturadores RT27](procedimentos/deploy-idmc-netsms-faturadores-rt27.md) | Import de 4 assets + query model, default e `.param` no servidor | [docx](evidencias/93480/evidencia_93480.docx) |
| 93639 | [Deploy Combo Multi Mobile NETSMS](procedimentos/deploy-idmc-combomulti-mobile-netsms.md) | Import com target sem `rt`, troca de conexão e runtime `Claro ICS` | [docx](evidencias/93639/evidencia_93639.docx) |
| 93584 | [Deploy Móvel RT27 Faturador Pré-Pago](procedimentos/deploy-movel-rt27-faturador-prepago.md) | Deploy de JARs em WebLogic (planta 4); não é asset IDMC | [docx](evidencias/93584/evidencia_93584.docx) |

## Procedimentos operacionais

| Tema | Documento | Descrição |
|------|-----------|-----------|
| Monitoramento | [Secure Agent](procedimentos/monitoramento-secure-agent.md) | Verificar status do agente e de seus serviços |
| Logs | [Checagem de logs](procedimentos/checagem-de-logs.md) | Onde e como consultar logs de jobs e do agente |
| Erros | [Tratamento de erros de integração](procedimentos/tratamento-erros-integracao.md) | Triagem e ações para falhas em tarefas/mapeamentos |

## Convenções

- Um procedimento por arquivo, em Markdown, nomeado em `kebab-case`, com Objetivo, Pré-requisitos, Passo a passo e Validação ([template](procedimentos/_template-procedimento.md)).
- Evidências ficam em `evidencias/<nº da change>/`; o runbook correspondente deve linkar o documento.
- Sempre confirmar **planta/ambiente, projeto de destino e conexões** na change e no manual antes de executar.
- Não registrar senhas, tokens ou dados sensíveis nos documentos (credenciais ficam no KeePass).
