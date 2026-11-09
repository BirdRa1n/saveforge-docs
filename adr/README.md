# Architecture Decision Records — SaveForge

Este diretório reúne as decisões que afetam mais de um repositório. As ADRs locais de cada repositório ficam em `docs/adr/` dentro dele.

Cada ADR segue o formato Contexto → Decisão → Consequências → Alternativas. O status evolui de `Proposta` para `Aceita`, `Rejeitada` ou `Substituída por NNNN`.

| ADR | Título | Status |
|---|---|---|
| [0001](0001-qt-quick-qml.md) | Qt Quick/QML para a UI do Desktop | Proposta |
| [0002](0002-cpp20-qt6-toolchain.md) | C++20, Qt 6.8+, CMake e vcpkg | Proposta |
| [0003](0003-vault-content-addressed.md) | Vault local com endereçamento por conteúdo | Proposta |
| [0004](0004-gamesave-zip.md) | `.gamesave` como contêiner ZIP | Proposta |
| [0005](0005-perfis-declarativos.md) | Perfis declarativos + mecanismos embutidos | Proposta |
| [0006](0006-registry-estatico-assinado.md) | Registry estático assinado (TUF-lite) | Proposta |
| [0007](0007-supabase-rls-rpc.md) | Supabase direto com RLS + RPC; Edge Functions só quando necessário | Proposta |
| [0008](0008-ludusavi-upstream.md) | Ludusavi Manifest como canal upstream separado | Proposta |
| [0009](0009-login-desktop-pkce.md) | Login opcional no Desktop via OAuth PKCE + loopback | Proposta |

O detalhamento completo está em [`../planejamento/PLANEJAMENTO-TECNICO.md`](../planejamento/PLANEJAMENTO-TECNICO.md).
