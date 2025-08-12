# AIコーディングエージェント指針

本テンプレートは Markdown 原稿 (`input/`) をルール (`rules/slide_rules.md`, `rules/artifact_rules.md`) とテンプレート (`template.md`) に基づき GeminiまたはGitHub copilot + Marp CLI でスライド化する最小構成。ここでは現状ディレクトリ構成に即した運用知識のみを記す。

## ディレクトリ実態
- 原稿: `input/*.md`
- ルール: `guidance/slide_rules.md`, `guidance/artifact_rules.md`
- Gemini コマンド定義: `.gemini/commands/*.toml` (主: `generate-slides.toml`)
- GitHub copilot コマンド定義: `.github/prompts/*.prompt.md`
- テーマ: `.themes/theme.css` (旧説明の `themes/` ではなく先頭ドット付き)
- テンプレート例: `template.md`
- 中間生成/作業: `artifact/` (スライド整形中間 `artifact_番号.md` 等を置く想定)
- 最終出力: `output/` (PDF 他)
- 画像資産: `.images/` (デフォルト `logo.png`)

## 生成フロー (標準)
1. 原稿作成: `input/xxx.md` 報告の目的、相手、内容などを列挙したテキストファイルを作成。
2. 報告骨子を作成: Gemini CLIまたはGitHub copilotのカスタムコマンド(`/generate-artifact`)をプロジェクトルートで実行。
3. コマンド内ロジック: 原稿読込 → ルール適用 (`guidance/artifact_rules.md`) → 出力ファイル生成(`output/artifact.md`)
4. 報告資料を作成: Gemini CLIまたはGitHub copilotのカスタムコマンド(`/generate-slides`)をプロジェクトルートで実行。
5. コマンド内ロジック: 報告骨子読込 → ルール適用 (`guidance/slide_rules.md`) → テンプレ適用 (`template.md`) → 出力ファイル生成(`output/slide.md`)
6. 報告資料をレビュー: Gemini CLIまたはGitHub copilotのカスタムコマンド(`/review`)をプロジェクトルートで実行。
7. テーマ変更時は再実行必須。

## 修正すべき既知差異 (自動化時に留意)
- 中間ファイル配置は `artifact/` を優先。`output/` は最終成果物専用とする。

## Front‑matter 必須キー
`marp: true`, `theme: myTheme`, `paginate: true`。必要に応じて `author:` `footer:` を付与。欠落時はテンプレート適用で補完する方針。

## スライド内容整形方針 (概要)
- 1スライド1メッセージ。
- 冗長語削除/平易化/箇条書き短文化。
- 過剰項目 (箇条書き >7) は分割。
- タイトル30全角以内、サブタイトル15全角以内。

詳細規則は `guidance/slide_rules.md` を常に優先。

## 典型タスクと行動
- 新規原稿: `input/new.md` 作成 (必要なら `template.md` 参照)。
- テーマ調整: `.themes/theme.css` 編集後、再生成。
- ロゴ差替え: `.images/logo.png` 差替え。ファイル名変更時は CSS の `background-image` を同期。
- ページ番号/フッター変更: `.themes/theme.css` の該当セレクタを編集。

## 変更時注意
- `template.md` 変更は今後の新規原稿へ影響、既存生成済み PDF には影響なし。
- Cookiecutter 変数は展開後ファイルに埋め込み済みか確認し、残存プレースホルダは必要なら置換。

## 禁止/避ける事項
- 汎用的ベストプラクティス羅列。
- 絵文字。
- 不自然スペース混入。

## エージェント動作ガイド
- 最小差分編集を原則。
- パス/ファイル不整合を検知したら修正提案→即適用 (危険性低の場合)。
- 追加情報が欠ける場合のみ簡潔質問。

## 不確定点
- Marp 実行コマンド詳細（ラッパースクリプト等）が別途存在するならその検出後に追記。

以上を基準に自動化/編集を行うこと。差分起点での改善を継続する。