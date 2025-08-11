## Cookiecutter Slide Template – エージェント作業指針

目的: Gemini CLI + Marp を用いたスライド生成プロジェクト用 Cookiecutter テンプレートを素早く拡張 / 保守できるようにする。

### 全体像
- これは Cookiecutter テンプレート。`cookiecutter gh:fktk/cookiecutter-slide` 実行後 `folder_name` で指定したディレクトリが生成。
- 生成プロジェクトの基本フロー: (1) `input/` に下書き Markdown → (2) Gemini コマンドでスライド整形 (ルール+プロンプト) → (3) Marp で PDF 化し `output/` に出力 → (4) レビュー & 再生成。
- カスタマイズ焦点: `themes/theme.css` (見た目) / `template.md` (初期スライド骨組み) / Gemini 用コマンド & ルール / `cookiecutter.json` 変数。

### 主要ファイル / 役割
- `cookiecutter.json`: 変数 `folder_name`, `author`, `organization` 定義。追加時はここ→テンプレート内で `{{cookiecutter.var}}`。
- `{{cookiecutter.folder_name}}/template.md`: 先頭 front‑matter 必須 (`marp: true`, `theme: myTheme`) を保持。
- `{{cookiecutter.folder_name}}/themes/theme.css`: 独自テーマ。`/* @theme myTheme */` と `@import "gaia"` 維持。背景ロゴは `./.images/logo.png`。
- `{{cookiecutter.folder_name}}/GEMINI.md`: 思考は英語 / 応答は日本語 / 絵文字禁止 / 日本語余分スペース禁止の運用規則。
- `.github/prompts/generate-slides.prompt.md`: 最小エージェントプロンプト (将来 `.gemini/commands/generate-slides.md` へ発展想定)。
- ルート `README.md`: インストール & 生成手順。生成ディレクトリ内 `README.md` が実行手順詳細。

### ワークフロー留意点 (自動化/保全)
1. 原稿: `input/` に Markdown 下書き配置。
2. 想定コマンド: `gemini -c .gemini/commands/generate-slides.toml input/<file>.md`。
3. コマンド側で `.gemini/rules/slide_rules.toml` を適用し構造化 → Marp 連携して PDF 出力。
4. テーマ・フッター値は Cookiecutter 変数依存。変数参照を文字列に潰さない。

### 変数追加手順
1. `cookiecutter.json` にデフォルト値付きで追加。
2. 利用箇所へ `{{cookiecutter.new_var}}` を挿入。
3. 未使用/廃止変数が残れば削除 (差分で検知)。

### テーマ / スタイル指針
- `/* @theme name */` コメント必須。削除すると Marp が認識しない。
- ページ番号: `section::after` の `attr(data-marpit-pagination)` を維持。
- ロゴパス変更ニーズが頻出したら将来変数化 (現状は記述のみ)。

### 言語 / 表記規則
- 日本語: 不要な ASCII スペースを入れない (例: "Claude Code入門").
- 絵文字禁止。生成された場合は除去。

### 典型的改善ポイント
- `.gemini/commands` / `.gemini/rules` ディレクトリ未整備なら雛形生成 (コメントで TODO 表示)。

### 安全な変更指針
- 固定パス直書きを避け `{{cookiecutter.folder_name}}` 変数利用。
- ルール文書 (安定) とコマンド (エントリポイント) を分離。混在させない。
- README と GEMINI.md の内容重複を増やさず参照に留める。

### スライド骨組み追加例
`template.md` に以下を `---` 区切りで挿入:
```markdown
---
## Agenda
- 背景
- 目的
- 次のステップ
```
先頭 front‑matter ブロックは必ず最初に残す。

### バリデーションヒント
- CSS/テンプレート変更後: サンプル Markdown で Marp ビルド (構文/パスエラー検出)。
- 参照している `{{cookiecutter.*}}` が `cookiecutter.json` に全て存在するか確認。
- UTF-8 維持 (BOM 付与しない)。

### 将来拡張 (黙って実装しない)
- ロゴパス変数化
- Gemini + Marp 実行を一括する Makefile / スクリプト
- `.gemini` 構成をテンプレート側で初期生成

### 判断不確実な場合
- 小さく可逆的に変更しコメントで疑問点を明示。
- 欠落構成 (例: `.gemini/commands`) は推測生成ではなく TODO で指摘。

不明点や追加したい規約があればフィードバックしてください。
