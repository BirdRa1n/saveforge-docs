# ADR 0004 — `.gamesave` como contêiner ZIP

**Status:** Proposta · **Data:** 2026-11-09

## Decisão
Um arquivo `.gamesave` é um ZIP (deflate) com:
1. `mimetype` como primeira entrada, sem compressão (STORED), contendo `application/vnd.savevault.gamesave+zip`;
2. `manifest.json` (schema `gamesave/manifest.v1`) e `manifest.json.sha256`;
3. `blobs/<sha256>`, deduplicados.

Os caminhos ficam sempre em forma de template, com placeholders. A importação valida hashes e schema e protege contra zip-slip e zip bomb. Importar **não** restaura nada. O modo incremental usa `baseExportId`. A biblioteca escolhida é a minizip-ng.

## Consequências
- (+) Pode ser inspecionado em qualquer SO, tem acesso aleatório e é amplamente suportado.
- (−) A compressão é inferior à do zstd. Isso é aceitável, porque saves costumam já ser compactos.

## Alternativas
- **tar.zst:** não abre nativamente no Windows.
- **Formato binário próprio:** exige construir ferramentas próprias.
- **SQLite como contêiner:** pouco amigável para inspeção manual.
