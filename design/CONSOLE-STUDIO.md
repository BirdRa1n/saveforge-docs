# Direção visual: Console × Studio

> **Status:** escolhida em 2026-11-10. Substitui a [Forja](FORJA.md) no SaveVault Desktop.
> As seis propostas comparadas ficaram no canvas "Propostas de interface"; esta é a proposta 6.

Esta direção junta as duas propostas preferidas:

- **Studio:** densidade e precisão, com uma lista que mostra tudo de uma vez e uma barra de busca no topo.
- **Console:** destaque para o jogo selecionado, ações grandes e navegação pelo teclado (e, no futuro, pelo controle).

As superfícies são neutras, em cinza-azulado, com variantes clara e escura. A cor fica a cargo do jogador, que escolhe o acento.

## Estrutura da janela

| Região | Conteúdo |
|---|---|
| Barra de título | Unificada (32 px). No Windows e no macOS, o logo e a busca (`Ctrl+K`) ficam na própria faixa do sistema, ao lado dos botões nativos da janela (veja a ADR 0006 do Desktop). Arrastar a área vazia move a janela, e o duplo clique maximiza. |
| Trilho de navegação | Ícones de 44 px com tooltip: Biblioteca, Atividade, Importar/Exportar, Configurações. |
| Painel de conteúdo | Superfície `bg` com o canto superior esquerdo arredondado (`radiusPanel`). |
| Barra de atalhos | Atalhos da página atual e, à direita, o estado do backup automático e do vault. |

A **Biblioteca** divide o painel em duas partes:

- **Lista densa (≈42%):** linhas de 52 px com miniatura, nome, loja, número de backups e status. O status é sempre um ponto colorido acompanhado de texto.
- **Painel do jogo:**
  - banner com a arte do jogo, ou a cor dele com as iniciais;
  - selo "Protegido";
  - ações com atalho: `Ctrl+B` backup, `Ctrl+R` restaurar, `Ctrl+T` trocar save;
  - quatro números, os saves com nome e o histórico.

## Cores

Os tokens ficam em `src/app/qml/theme/Theme.qml`. Os componentes usam só esses tokens.

| Token | Escuro | Claro | Uso |
|---|---|---|---|
| `window` | `#0F1218` | `#E9EDF2` | moldura: barra de título, trilho, barra de atalhos |
| `bg` | `#151922` | `#FFFFFF` | painéis de conteúdo |
| `card` / `surface` | `#1B2029` | `#F6F8FA` | cards, números, diálogos |
| `surfaceRaised` | `#222834` | `#EEF1F5` | hover |
| `border` | branco 8% | tinta 10% | divisórias |
| `text` | `#ECEFF4` | `#121620` | texto principal |
| `textMuted` | `#A3ACBA` | `#4F5868` | texto secundário |
| `textSubtle` | `#8D96A5` | `#5F6878` | metadados |
| `accent` | escolha do usuário | escolha do usuário | ação primária, seleção, save em uso |
| `accentTint` | acento 14% | acento 12% | fundo do item selecionado |
| `textOnAccent` | calculado | calculado | tinta escura em acentos claros e branco nos escuros |
| `accentText` | acento | acento escurecido | acento usado como texto, legível no tema claro |

**Acentos oferecidos:**

- Ciano `#22D3EE` (padrão)
- Azul `#3B82F6`
- Violeta `#8B5CF6`
- Verde `#22C55E`
- Laranja `#F97316`
- Rosa `#EC4899`

O tema pode seguir o sistema, ou ser fixado em escuro ou claro, em Configurações › Aparência.

## Tipografia

Todas as fontes usam a licença SIL OFL e vêm embutidas no app.

| Papel | Fonte |
|---|---|
| Títulos | Outfit 700 |
| Texto e interface | Inter 400/500/600 |
| Números, datas, atalhos | JetBrains Mono 400/500 |

| Papel | Tamanho |
|---|---|
| Título de página | 26 px |
| Título de seção | 18 px, ou rótulo em maiúsculas de 12 px |
| Corpo | 13–14 px |
| Metadados | 12 px |

## Forma

- **Raios:**
  - 6 px: badges
  - 8 px: controles
  - 12 px: cards
  - 14 px: painel
  - pílula: chips
- **Espaçamento:** a escala continua 4, 8, 12, 16, 20, 24 e 32.
- **Foco:** contorno de 2 px no acento. O item selecionado da lista usa o mesmo contorno, então a seleção e o foco do teclado são uma coisa só.
- **Uso do acento:** um elemento cheio por região, que é a ação principal ou o chip ativo. A seleção usa só o tom (`accentTint`).
