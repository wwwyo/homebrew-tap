# homebrew-tap

Homebrew tap for [wwwyo](https://github.com/wwwyo)'s command-line tools.

## Formulae

| Formula | Description | Source |
|---|---|---|
| `syokan` | LLMs summon rich UI: post a JSON tree, an ephemeral view appears | [wwwyo/syokan](https://github.com/wwwyo/syokan) |
| `skillctrl` | Manage agent skills while preserving local adaptation intent | [wwwyo/skillctrl](https://github.com/wwwyo/skillctrl) |

## Install

```bash
brew install wwwyo/tap/syokan
brew install wwwyo/tap/skillctrl
```

Formulae here install prebuilt binaries for macOS (arm64 / x86_64) and Linux (arm64 / x86_64). Windows is not supported.

Every formula is generated in its own project. Syokan's release workflow pushes updates automatically. Skillctrl publishes a generated formula as a release asset; its maintainer copies that asset here after verifying the release checksums. Do not edit `Formula/*.rb` in this repository — see [AGENTS.md](./AGENTS.md).
