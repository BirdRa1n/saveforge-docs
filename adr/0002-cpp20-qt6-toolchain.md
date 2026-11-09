# ADR 0002 — C++20, Qt 6.8+, CMake e vcpkg

**Status:** Proposta · **Data:** 2026-11-09

## Decisão
- **C++20** (concepts, ranges, `std::span`, designated initializers). C++23 só será adotado quando o suporte for uniforme em MSVC, GCC e AppleClang.
- **Qt 6.8 como versão mínima**, com builds oficiais na versão estável mais recente (hoje 6.12). Para usuários open source, as correções do Qt chegam pelas versões novas, e não por patches das LTS.
- **CMake ≥ 3.24** com `CMakePresets.json`, `qt_standard_project_setup()` e `qt_add_qml_module()`.
- ~~**vcpkg** (modo manifest) para as dependências não-Qt: zstd, libsodium, minizip-ng e qtkeychain.~~ **Ajustado em 2026-11-09:** as dependências não-Qt usam primeiro a versão do sistema (`find_package`) e, se ela não existir, baixam um release fixado com verificação de SHA-256 via `FetchContent`. O vcpkg continua funcionando como toolchain opcional, mas não é obrigatório. Detalhes em `saveforge-desktop/docs/adr/0001-third-party-dependencies.md`.
- Compiladores: MSVC 2022 (release no Windows), MinGW (desenvolvimento), GCC ≥ 12 e Clang/AppleClang ≥ 15.
- Cada módulo de `src/` é uma biblioteca estática, com regra de dependência unidirecional (ver §5.1 do plano).
- Os erros usam um tipo `Result<T, Error>` próprio. Exceções não cruzam fronteiras de módulo.

## Consequências
- (+) Linguagem moderna com suporte amplo nos três SOs.
- (−) O MSVC continua sendo o alvo de release no Windows; o MinGW é suportado para desenvolvimento.

## Alternativas
- **C++17:** menos expressivo.
- **C++23:** suporte ainda desigual entre os compiladores.
- **Conan:** é uma boa opção, mas o vcpkg se integra melhor com presets e com o CI do GitHub.
