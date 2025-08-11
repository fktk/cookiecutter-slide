---
mode: 'agent'
description: 'コンテンツを読んで、報告の骨子を生成'
---

## Context
- ガイドライン: [rules/artifact_rules.md](rules/artifact_rules.md)
- 入力ファイル: [input/*.md](input/*.md)

## タスク
1. 入力Markdownファイルを読む。
2. ガイドラインを読む。
3. ガイドラインに従って報告骨子のMarkdownを生成。
6. ファイル (`artifact/artifact_(01-10).md`) に保存する。(01-10は自動で付与)