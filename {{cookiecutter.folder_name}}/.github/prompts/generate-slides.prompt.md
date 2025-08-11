---
mode: 'agent'
description: '報告骨子を簡素化してスライドを生成'
---

## Context
- ガイドライン: [rules/slide_rules.md](rules/slide_rules.md)
- テンプレート: [template.md](template.md)
- 入力ファイル: [artifact/*.md](artifact/*.md)

## タスク
1. 入力Markdownファイルを読む。
2. スライドガイドラインを読む。
3. ガイドラインに従ってMarkdown内容を簡素化（冗長表現削除・要約・箇条書き化・1スライド1主題）。
4. テンプレートを読む。
5. 簡素化後コンテンツへテンプレートを適用（必要なfront-matterと区切りを整える）。
6. ファイル (`output/slides.md`) に保存する。