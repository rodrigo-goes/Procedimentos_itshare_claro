# Deploy Móvel – RT27 Faturador Pré-Pago (Planta 4)

- **Change/evidência:** 93584 – [evidencia_93584.docx](../evidencias/93584/evidencia_93584.docx)
- **Equipe/Projeto:** Móvel – Reforma Tributária 2027 (RT27)
- **Produto:** FATURADOR PREPAGO (Pré, Controle Fácil, IoT, Flex, MVNO)
- **Servidor:** `CBC2CM48600` (aplicação, planta 4), usuário `weblogic`
- **Executado em:** 23/10/2026
- **Última atualização:** 2026-10-27

> Este deploy é de aplicação (JARs em WebLogic), não de assets IDMC. Fica nesta pasta por pertencer ao mesmo conjunto de changes do repositório.

## Objetivo

Atualizar os JARs do faturador Pré-Pago da Móvel (RT27) na planta 4, com backup prévio, permissões padronizadas e evidências.

## Contexto

- A Claro tem equipes **Móvel** e **Residencial**. Pré-Pago, Controle Fácil, IoT, Flex e MVNO são da **Móvel**.
- O mesmo projeto (RT27) pode rodar em várias plantas; **confirmar sempre a planta na change** (aqui, planta 4).
- Não confundir o projeto **NFCOM** com **Reforma Tributária**: são projetos distintos.

## Pré-requisitos

- Change aberta no CTC (campos: ambiente `AMBIENTE4`, aplicação `FATURADOR PREPAGO`, janela prevista, anexos).
- Manual de instalação anexo à change e os pacotes da versão (Nexus `.../Movel/NOTA/NFCOMPREPAGO/v<versão>/`): `RT27_CF_bin.zip`, `RT27_Flex_bin.zip`, `RT27_MVNO_bin.zip`, `RT27_PRE_PAGO_bin.zip`.
- Acesso via WinSCP ao servidor com o usuário `weblogic` (credencial no KeePass, conforme o CTC).
- Pasta local de trabalho com o número da change (ex.: `93584`).

## Passo a passo

1. Abrir a change no CTC e conferir planta, aplicação e anexos.
2. Abrir o manual anexo e identificar os arquivos e diretórios do deploy.
3. Baixar os 4 pacotes (`RT27_*_bin.zip`) para a pasta local e extrair.
4. Conectar ao servidor `CBC2CM48600` como `weblogic`; confirmar que o **owner** dos arquivos é `weblogic`.
5. **Backup:** em cada diretório, renomear o JAR e o `.md5` atuais com o padrão `<arquivo>_<nº change>_<DDMMAAAA>`, por exemplo `NFComCFPosPago.jar_93584_23102026` e `NFComCFPosPago.jar.md5_93584_23102026`.

   | Componente | Diretório (`/PROD_CLARO/PPY/...`) | Arquivos |
   |------------|-----------------------------------|----------|
   | CF Pós-Pago | `NFCOM_CF_POS_PAGO/bin` | `NFComCFPosPago.jar` e `.md5` |
   | Flex | `NFCOM_FLEX/bin` | `NFComFlex.jar` e `.md5` |
   | MVNO | `NFCOM_MVNO/bin` | `NFComMvno.jar` e `.md5` |
   | Pré-Pago | `NFCOM_PRE_PAGO/bin` | `NFComPrePago.jar` e `.md5` |

   > O manual cita `/PRODCLARO/PPY/...`; o servidor mostra `/PROD_CLARO/PPY/...` (com underscore) e `NFCOM_PRE_PAGO`. Seguir o caminho real do servidor.
6. **Copiar** os novos JAR e `.md5` de cada pacote para o respectivo `bin`.
7. **Permissões:** os arquivos novos devem ficar com **775** (`Properties` > Octal `0775`), owner/group `weblogic`.
8. Capturar prints de cada etapa (backup, cópia, permissões) e anexar ao documento Word de evidência.

## Validação

- Em cada `bin`: JAR e `.md5` novos com data/hora do deploy, tamanho coerente com o pacote e permissão 775.
- Cópias de backup com o sufixo `_93584_23102026` presentes.
- Prints anexados ao [documento de evidência](../evidencias/93584/evidencia_93584.docx) e change atualizada no CTC.

## Observações da evidência

- No `NFCOM_MVNO/bin`, o backup do `.md5` aparece como `..._93585_23102026`, enquanto o do JAR aparece como `..._93584_23102026`. Conferir o número da change nos nomes de backup para evitar esse tipo de divergência.
- No `NFCOM_PRE_PAGO/bin` há backups antigos com permissão `rw-rw-r--`; os arquivos desta change devem ficar em 775.

## Rollback / Escalonamento

- Renomear de volta os arquivos `_93584_23102026` para os nomes originais (JAR e `.md5`) e validar com o time responsável. Dúvidas sobre planta ou pacote: acionar o solicitante da change.

## Referências

- [Export/Import de assets IDMC](export-import-assets-idmc.md) (para changes IDMC)
