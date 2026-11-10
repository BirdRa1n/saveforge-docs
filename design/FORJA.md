# Direção visual: Forja

> **Status:** escolhida em 2026-11-09. No SaveVault Desktop, foi substituída em 2026-11-10 pela [Console × Studio](CONSOLE-STUDIO.md). Continua sendo a referência do SaveVault Community.
> As propostas originais estão no canvas "SaveVault — Propostas de design".

A interface é escura e quente, com acento de brasa laranja. A ideia é transmitir solidez: algo construído para durar.

## Cores

| Token | Valor | Uso |
|---|---|---|
| `bg` | `#16130F` | fundo da janela/página |
| `surface` | `#1E1A15` | barra lateral, cabeçalhos |
| `card` | `#1F1A14` | cards de jogo, painéis |
| `surfaceRaised` | `#251F18` | blocos de destaque dentro de superfícies |
| `control` | `#221D17` | campos e botões secundários |
| `selected` | `#2A231B` | item de navegação ativo |
| `border` | `#2E2820` | divisórias |
| `borderStrong` | `#3A3127` | bordas de controles |
| `text` | `#F5EFE6` | texto principal |
| `textMuted` | `#BFB3A3` | texto secundário, navegação inativa |
| `textSubtle` | `#A89C8C` | metadados (loja, datas) |
| `accent` | `#F97316` | ação primária, logo, foco |
| `textOnAccent` | `#1A1208` | texto sobre o acento |
| `accentSoft` | `#FDBA74` | links |
| `successBg` / `successFg` | `#1F3324` / `#86EFAC` | "Protegido", "Backup há…" |
| `warningBg` / `warningFg` | `#3A2A12` / `#FCD34D` | conflitos (ex.: Steam Cloud) |
| `neutralBg` / `neutralFg` | `#2E2820` / `#D6CBBD` | "Sem backup", pendente |

Os status nunca dependem só da cor: cada um tem também um rótulo em texto.

## Tipografia

- **Títulos:** Space Grotesk 700, com letter-spacing −0.02em.
- **Texto e UI:** Inter 400/500/600.
- As duas fontes usam a licença SIL OFL. No Desktop, elas serão empacotadas como recurso do aplicativo (pendente). Até lá, o app usa a fonte do sistema.

| Papel | Tamanho |
|---|---|
| Título de página | 30 px |
| Título de seção | 20 px |
| Corpo | 14–15 px |
| Metadados | 12–13 px |

## Forma e espaçamento

- Escala de espaçamento: 4, 8, 12, 16, 20, 24, 32.
- Raios: 6 px (badges), 10 px (controles e itens de navegação), 14 px (cards), 999 px (chips de filtro).
- Alvos de clique ≥ 44 px de altura.
- O acento aparece em um elemento por região: a ação primária ou o item selecionado. Nunca em fundos grandes.

## Componentes de referência

- **Barra lateral:** logo, navegação (Biblioteca, Atividade, Importar/Exportar, Configurações) e um bloco de status do vault no rodapé.
- **Card de jogo:** capa (ou bloco de cor com iniciais quando não há capa), nome, loja e badge de status.
- **Chips de filtro:** o chip ativo é preenchido com `text`; os inativos ficam só com contorno.
- **Botão primário:** fundo `accent` e texto `textOnAccent`. O botão secundário usa `control` e `borderStrong`.
