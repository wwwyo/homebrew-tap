# homebrew-tap

Homebrew tap that distributes [syokan](https://github.com/wwwyo/syokan). This repository stores exactly one artifact — the formula — and holds no build, no dependencies, and no generation logic of its own.

## ディレクトリ構造

```
homebrew-tap/
└── Formula/
    └── syokan.rb   # generated. Never edit by hand
```

## Formula は生成物であり、ここでは編集しない

`Formula/syokan.rb` は syokan 側の release workflow が生成して push する。生成器は [apps/syokan/scripts/generate-formula.ts](https://github.com/wwwyo/syokan/blob/main/apps/syokan/scripts/generate-formula.ts) で、release asset の `checksums.txt` から各 OS/arch の URL と sha256 を埋める。

生成を一方向（syokan → tap）に閉じているのは、tap 側で手編集すると次の release で無言のうちに上書きされ、編集内容と履歴の両方が失われるため。formula を変えたい場合は **generate-formula.ts を直す**。

したがってこの repo で行う正当な変更は次に限られる:

- README.md / AGENTS.md の更新
- syokan 側で generate-formula.ts を直したうえでの、release 経由の formula 更新

## セットアップ

配布物のみでツールチェーンを持たないため、install するものは無い。tap の動作確認は Homebrew で行う。

```bash
brew tap wwwyo/tap
brew install wwwyo/tap/syokan
brew test syokan
```

## 更新フロー

syokan で `bun run release` を実行して version tag を push すると、CI が build → smoke → publish と進み、最後の homebrew job がこの repo の `Formula/syokan.rb` を書き換えて commit する。tap 側でメンテナが叩くコマンドは無い。

job は fine-grained PAT（この repo のみ / contents:write）を syokan 側の `TAP_GITHUB_TOKEN` secret から使う。formula が前回と同一内容のときは commit を skip するため、job の再実行は安全に繰り返せる。
