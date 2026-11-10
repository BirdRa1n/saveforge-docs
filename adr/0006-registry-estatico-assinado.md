# ADR 0006 — Registry estático assinado (TUF-lite)

**Status:** Proposta · **Data:** 2026-11-09

## Decisão
- O Registry é **código-fonte em Git** (`savevault-registry`). O CI compila bundles JSON (zstd) por canal e os publica em hospedagem estática: GitHub Pages como primário, GitHub Releases e R2 como mirrors.
- A assinatura usa **Ed25519 (libsodium)** em duas camadas:
  - a(s) **chave(s) raiz, offline**, assinam o `root.json`, que lista as chaves online e sua expiração;
  - a **chave online**, guardada como secret do GitHub Actions em um environment protegido, assina o `index.json`.
- O `index.json` contém uma `sequence` monotônica (anti-rollback), um `expires` (anti-freeze), o hash e o tamanho do bundle e uma lista `revoked`.
- O cliente verifica tudo antes de trocar o cache e mantém os 3 últimos bundles, de modo que nunca fica sem perfis. Uma expiração gera aviso, não bloqueio.
- Um rollback é publicado como nova sequência com o conteúdo revertido.

## Consequências
- (+) Independente do website e do Supabase, com CDN barata e funcionamento offline pelo cache.
- (+) Comprometer o Supabase ou a CDN não permite distribuir perfis.
- (−) A gestão de chaves exige disciplina. O procedimento será documentado em `savevault-registry`.

## Alternativas
- **Servir via Supabase ou API própria:** acopla o Desktop ao backend.
- **Git como transporte no cliente:** pesado.
- **TUF completo:** não há implementação C++ madura.
