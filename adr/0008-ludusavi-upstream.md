# ADR 0008 — Ludusavi Manifest como canal upstream separado

**Status:** Proposta · **Data:** 2026-11-09

## Contexto
O Ludusavi Manifest cobre milhares de jogos e é a forma mais rápida de oferecer cobertura útil desde o primeiro release. O código dele é MIT. Os dados são compilados da PCGamingWiki, cujo conteúdo é licenciado como **CC BY-NC-SA 3.0** (segundo fontes secundárias; conferir no rodapé do wiki).

Essa licença **permite** que o SaveForge use os dados, com três condições:
- **atribuição:** dar crédito à PCGamingWiki e ao Ludusavi Manifest;
- **uso não comercial:** não vender os dados nem usá-los em um recurso pago;
- **compartilhar igual:** redistribuir os dados e qualquer modificação deles sob a mesma licença.

A licença dos dados não afeta a licença do código do app, que continua MIT.

## Decisão
- O CI do Registry fixa um commit upstream em `upstream/ludusavi.lock.json`. Um PR automático semanal atualiza esse commit, e a mudança passa por revisão.
- Um conversor gera perfis `profile.v1` e os publica no canal **`upstream-ludusavi`**, separado do `official`, **sob CC BY-NC-SA 3.0**. O bundle carrega a atribuição e o texto da licença, e cada perfil tem `provenance.source = ludusavi`.
- A atribuição também aparece na tela "Sobre" do Desktop e no site da Community.
- Nenhum recurso pago futuro depende desse canal sem autorização da PCGamingWiki.
- Um perfil oficial substitui o perfil upstream do mesmo jogo.
- O Desktop lê apenas JSON assinado, sem parser YAML no cliente.

## Consequências
- (+) Cobertura imediata, licenças claramente separadas e a mesma verificação de integridade dos perfis oficiais.
- (−) Dependência do formato upstream, mitigada por testes de snapshot do conversor.
- (−) Um perfil oficial criado **a partir** de dados do Ludusavi herda o CC BY-NC-SA. Só perfis escritos do zero, como correções originais da comunidade, podem usar a licença própria do Registry. O campo `provenance.basedOn` registra essa origem.

## Alternativas
- **O Desktop baixar o YAML diretamente do GitHub do Ludusavi:** sem assinatura do SaveForge e com parser YAML em C++.
- **Importar os dados para o canal `official`:** mistura licenças.
