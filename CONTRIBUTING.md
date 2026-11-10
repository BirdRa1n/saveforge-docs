# Contribuindo com o saveforge-docs

Este repositório guarda a documentação **transversal** do ecossistema SaveForge: planejamento técnico, ADRs que afetam mais de um repositório e o guia visual.

## O que vai em cada pasta

| Pasta | Conteúdo |
|---|---|
| `planejamento/` | Planejamento técnico e roadmap |
| `adr/` | Architecture Decision Records que afetam mais de um repositório |
| `design/` | Direções visuais (Console × Studio no Desktop, Forja no Community), com tokens e regras de componentes |

As ADRs que afetam um único repositório ficam em `docs/adr/` dentro desse repositório. Os formatos normativos (schemas, specs) ficam em `saveforge-specs`.

## ADRs

- Numeração sequencial (`NNNN-titulo-curto.md`), sem reaproveitar números.
- Estrutura: Contexto → Decisão → Consequências → Alternativas.
- O status vai de `Proposta` para `Aceita`, `Rejeitada` ou `Substituída por NNNN`. Uma ADR aceita não é reescrita: ela é substituída por uma nova.
- Toda ADR nova entra no índice `adr/README.md`.

## Estilo

- Documentação em **pt-BR**, objetiva e para dois públicos: pessoas e agentes de IA.
- Use tabelas para comparações e diagramas Mermaid para fluxos.
- Links relativos entre documentos.

## Commits

[Conventional Commits](https://www.conventionalcommits.org/) **em inglês**, no imperativo e com até 72 caracteres no assunto. Por exemplo: `docs(adr): add ADR 0010 for cloud storage backends`.

Não adicione trailers de coautoria de ferramentas de IA.
