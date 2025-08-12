# プレゼンテーション資料テンプレート (`{{cookiecutter.folder_name}}`)

Markdown 原稿 + ガイダンス + テンプレートを Gemini / Copilot + Marp CLI でスライド化する最小構成です。

## ディレクトリ概要
- 原稿: `input/*.md`
- ルール: `guidance/slide_rules.md` (簡素化ガイド)
- テンプレート: `template.md`
- テーマ: `.themes/theme.css`
- 中間生成: `artifact/` (整形途中の `artifact.md` など)
- 出力: `output/` (最終 PDF 等)
- 画像: `.images/logo.png`

## 利用手順
### 1. ロゴ準備
`.images/` にロゴ画像を配置 (既定名 `logo.png`)。名称変更時は `.themes/theme.css` の `background-image` を同期。

### 2. 原稿作成
`input/your.md` を作成。ページ区切りが必要なら `---`。見出しは `#`/`##` を基本に構造化。

### 3. スライド整形 (中間Markdown生成)
Gemini CLI で簡素化 + テンプレ適用 (コマンド例):

```bash
gemini -c .gemini/commands/generate-slides.toml input/your.md
```

処理内容 (generate-slides):
1. 入力Markdown読込。
2. `guidance/slide_rules.md` を適用し簡素化 (冗長削除/1スライド1メッセージ化)。
3. `template.md` の front‑matter を補完。
4. 整形結果を `artifact/slides.md` へ出力。

### 4. PDF 生成
`artifact/slides.md` を Marp CLI で PDF 化 (例。環境により調整):

```bash
marp --theme .themes/theme.css --pdf artifact/slides.md -o output/slides.pdf
```

### 5. 成果物確認
`output/` 内の PDF を閲覧。

## カスタマイズ
- テーマ変更: `.themes/theme.css` を編集後、整形→PDF 手順を再実行。
- Front‑matter 追加: `author:` `footer:` などを `template.md` へ記述 (既存出力へは後追い適用なし)。
- スライド分割調整: 行数や箇条書きが多い場合は原稿へ `---` を追加し分割。

## ガイド (抜粋)
- 1スライド1メッセージ / 箇条書き 5〜7 項目以内。
- タイトル 30 全角以内 / サブタイトル 15 全角以内。
- 不要な冗長語・重複を削除し簡潔化。
詳細は `guidance/slide_rules.md` を参照。

## よくある変更
| 目的 | 操作 |
|------|------|
| ロゴ差替え | `.images/logo.png` を置換 + CSS パス確認 |
| 色/フォント変更 | `.themes/theme.css` を編集 |
| ページ番号/フッター | `.themes/theme.css` の該当セレクタを編集 |
| 新規スライド | `input/new.md` 作成 → 手順 3 へ |

## 注意事項
- `.themes/theme.css` 編集後は PDF 再生成が必要。
- 既存 PDF に retroactive な自動更新は行われない。
- `output/` は最終成果物専用。中間ファイルは `artifact/` に置く。

## 制約 / 禁止
- 絵文字多用・冗長一般論の記述を避ける。
- 日本語文中に不要スペースを入れない。

## トラブルシュート
- テーマ反映されない: コマンドで `--theme .themes/theme.css` を指定しているか確認。
- 画像表示されない: 相対パス `.themes/theme.css` 内の `url(../.images/logo.png)` 等パス整合を確認。

---
最小構成を保ちつつ必要に応じ段階的改良を行ってください。
