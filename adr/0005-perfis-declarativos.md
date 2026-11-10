# ADR 0005 — Perfis declarativos + mecanismos embutidos

**Status:** Proposta · **Data:** 2026-11-09

## Contexto
O requisito é não executar código arbitrário vindo da comunidade e, ainda assim, suportar jogos com armazenamento atípico.

## Decisão
- Perfis são **dados**: escritos em YAML no Registry, distribuídos em JSON e validados por JSON Schema (`profile.v1`) e pelo lint de caminhos.
- Comportamentos especiais são **tipos de mecanismo embutidos no Desktop** (`standard`, `latest-n`, `store-user-scoped`), que o perfil seleciona e parametriza. Necessidades que combinam com qualquer mecanismo são opções do perfil, e não mecanismos: a seção `registry` (registro do Windows), `backup.consistentGroups` (leitura consistente de vários arquivos) e `backup.maxBytes` (limite de tamanho).
- Uma contribuição do tipo "novo mecanismo" vira uma proposta de funcionalidade, implementada em C++ e revisada no `savevault-desktop`.
- Se o perfil usar um tipo desconhecido, ele é ignorado com aviso. Nunca há interpretação parcial.
- A precedência é local > official > upstream-ludusavi, com substituição integral do perfil e sem mesclagem.

## Consequências
- (+) Não existe superfície de execução remota, e os perfis podem ser auditados em diff.
- (−) Casos novos exigem um release do Desktop. A mitigação é o campo `minAppVersion` no perfil.

## Alternativas
- **Scripts Lua/JS:** risco de segurança.
- **WASM em sandbox:** complexo. Só será reavaliado se surgir uma necessidade real.
