---
mode: 'agent'
description: 'コンテンツを読んで、報告の骨子を生成'
---

## Context
- ガイドライン: [rules/artifact_rules.md](rules/artifact_rules.md)
- コンテンツ: [input/*.md](input/*.md)

## タスク
1. 入力Markdownファイルを読む。
2. ガイドラインを読む。
3. ガイドラインに従って報告骨子のMarkdownを生成。
6. ファイル (`artifact/artifact_(番号).md`) に保存する。(番号は自動で付与)