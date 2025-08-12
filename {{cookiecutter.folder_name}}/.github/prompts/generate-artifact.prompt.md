---
mode: 'agent'
description: 'コンテンツを読んで、報告の概要、骨子を生成する'
---

## Context
- [コンテンツ](input/*.md)
- [ガイドライン](guidance/artifact_rules.md)

## タスク
1. コンテンツを読む。
2. ガイドラインを読む。
3. ガイドラインに従って報告の概要、骨子のMarkdownを生成する。
4. ファイル (`artifact/artifact_(番号).md`) に保存する。(番号は自動で付与)