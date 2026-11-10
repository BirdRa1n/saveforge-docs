# ADR 0009 — Login opcional no Desktop via OAuth PKCE + loopback

**Status:** Proposta · **Data:** 2026-11-09 · **Fase:** 5

## Decisão
- O login usa o fluxo **Authorization Code + PKCE** do Supabase Auth, aberto no **navegador do sistema** (nunca em WebView embutido), com redirecionamento **loopback** para `http://127.0.0.1:<porta-efêmera>/callback` (RFC 8252).
- O Desktop usa apenas a chave publishable. O refresh token fica no **cofre do SO** via QtKeychain (Credential Manager, Keychain ou Secret Service).
- O login é opcional e não habilita nem condiciona nenhuma função local.
- Na implementação, será preciso verificar se a allowlist de redirect do Supabase aceita porta curinga. Se não aceitar, a alternativa é uma porta fixa configurável ou o esquema `savevault://`.

## Consequências
- (+) O usuário não digita senha no app, e esse é o padrão recomendado para apps nativos.
- (−) Firewall ou antivírus podem bloquear o loopback. Nesse caso, o fallback é o esquema customizado.

## Alternativas
- **Device authorization flow:** não é suportado nativamente pelo Supabase Auth.
- **Login com senha dentro do app:** má prática.
- **Esquema de URL customizado como opção principal:** exige registro diferente em cada SO.
