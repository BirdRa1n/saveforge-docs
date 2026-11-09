# ADR 0007 — Supabase direto com RLS + RPC; Edge Functions só quando necessário

**Status:** Proposta · **Data:** 2026-11-09

## Decisão
Cada operação usa a primeira opção que a resolver, nesta ordem:
1. **PostgREST + RLS** para CRUD simples. Todas as tabelas de `public` têm RLS.
2. **Funções Postgres (RPC, `security definer`, `search_path` vazio)** para operações transacionais e transições de estado: submeter, votar, revisar e conceder papéis. Colunas sensíveis, como `status` e os contadores, não aceitam `UPDATE` direto.
3. **Edge Functions** apenas para segredos e integrações externas: `publish-contribution` (GitHub App), `registry-sync` (webhook HMAC) e `game-metadata` (IGDB/SteamGridDB).

A validação de perfis acontece no banco, com **`pg_jsonschema`** e um lint em SQL. A autorização usa `user_roles` e `private.has_role()`. O schema `private` não é exposto pela API, e cada policy é coberta por testes pgTAP.

## Consequências
- (+) As regras são aplicadas no banco, um ponto único por onde toda requisição passa, com pouco código de servidor.
- (−) A lógica em PL/pgSQL exige testes pgTAP rigorosos e revisão cuidadosa das funções `security definer`.

## Alternativas
- **API REST própria:** duplica regras e aumenta a superfície de ataque.
- **Edge Functions para tudo:** mais latência e autorização duplicada.
