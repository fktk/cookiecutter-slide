---
mode: 'agent'
description: 'Markdownを簡素化してスライドを生成'
---

## Context
- Guidelines: [rules/slide-rules.md](rules/slide-rules.md)
- Template: [template.md](template.md)
- : [input/*.md](input/*.md)

## タスク
1. 入力Markdownファイルを読む。
2. スライドガイドラインを読む。
3. ガイドラインに従ってMarkdown内容を簡素化（冗長表現削除・要約・箇条書き化・1スライド1主題）。
4. デザインテンプレートを読む。
5. 簡素化後コンテンツへテンプレートを適用（必要なfront-matterと区切りを整える）。
6. 一時ファイル (例: `artifact/slides.md`) に保存する。