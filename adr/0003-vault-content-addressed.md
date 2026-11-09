# ADR 0003 — Vault local com endereçamento por conteúdo

**Status:** Proposta · **Data:** 2026-11-09

## Contexto
O vault precisa guardar o histórico de backups frequentes (automáticos) sem duplicar dados, resistir a interrupções e, no futuro, sincronizar com a nuvem.

## Decisão
- Cada blob recebe o nome do **SHA-256 do conteúdo original**, é comprimido com **zstd** e fica em `blobs/sha256/<2>/<hash>.zst`.
- Os **snapshots são imutáveis** e gravados em JSON (`snapshots/<game>/<uuidv7>.json`), com a lista `caminho-template → sha256`.
- **O SQLite é um índice reconstruível**, nunca a fonte da verdade, e fica fora do vault.
- A escrita é atômica (tmp + fsync + rename) e o snapshot é gravado por último. Uma coleta de lixo do tipo mark-and-sweep remove os blobs órfãos.

## Consequências
- (+) Backup incremental e deduplicação vêm de graça. Uma falha deixa, no máximo, blobs órfãos.
- (+) Como os arquivos são imutáveis, o vault é compatível com pastas sincronizadas e com object storage (Fase 6).
- (−) Arquivos grandes que mudam pouco são recopiados inteiros, porque não há chunking. Para saves isso é aceitável, e o chunking pode entrar em uma `vault v2`.

## Alternativas
- **restic/kopia embutidos:** são binários externos, com um formato fora do nosso controle.
- **Cópia por pasta datada:** sem deduplicação.
- **Blobs dentro do SQLite:** pior para arquivos grandes e para sincronização.
