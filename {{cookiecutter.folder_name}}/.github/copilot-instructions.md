# AI コーディングエージェント指針

本リポジトリは「Cookiecutter テンプレート化されたプレゼン資料生成環境」の雛形ディレクトリです。目的は: Markdown + テンプレート + ルールを用いて Gemini (LLM) と Marp CLI により PDF スライドを一貫生成すること。ここに記すのはこのテンプレート特有の知識のみです。汎用的アドバイスは不要。

## 全体像 (Big Picture)
- 入力: `input/*.md` (ユーザが書く原稿)。
- 変換ルール: `.gemini/commands/generate-slides.toml` (Gemini CLI コマンド) と `.gemini/rules/slide_rules.md` (スライド最適化ルール) — ※これらファイルは生成後環境に存在する想定。テンプレートでは README が手順と役割を説明。
- テーマ: `themes/theme.css` (Marp テーマ + ロゴ背景 + ページネーション生成)。
- テンプレート例: `template.md` (YAML front‑matter: `marp: true`, `theme: myTheme`, `paginate: true` など)。
- 出力: `output/*.pdf` (Marp CLI により生成)。
- 静的アセット: `.images/` (ロゴ等) — デフォルト参照ファイル `logo.png`。README にしたがい存在しない場合は追加が必要。

## 開発・利用ワークフロー
1. Markdown 原稿作成: `input/your.md` (見出しは `#`/`##` 区切り、ページ区切りは `---`)。
2. 生成実行: `gemini -c .gemini/commands/generate-slides.md input/your.md` をプロジェクトルートで実行。
3. Gemini コマンドは (a) 原稿読込 → (b) ルール適用 (`.gemini/rules/slide_rules.md`) → (c) Marp CLI 呼び出し (テーマ `themes/theme.css`) → (d) `output/` に PDF 書出。
4. テーマ調整: `themes/theme.css` を編集 (背景画像パス, 色, フッター, ページネーション)。

## プロジェクト固有ルール (GEMINI.md 抜粋反映)
- 絵文字禁止。出力/編集提案でも使用しない。
- 日本語文章内に不要なスペースを挿入しない (「Claude Code入門」のように)。
- 思考は英語/最終出力は日本語 (エージェント内部)。
- タスク完了時に完了通知コメント (本ガイドラインに準拠する他ツール連携時)。

## パターン / コンベンション
- スライド境界: Markdown の `---` でページ分割 (Marp 標準)。
- フロントマター必須キー: `marp: true`, `theme: myTheme`, `paginate: true`。`footer:` `author:` は Cookiecutter 変数で埋め込まれる。
- ページ番号は `theme.css` の `section::after` で自動挿入, 変更は CSS の `content` プロパティを編集。
- ロゴ画像パスは `themes/theme.css` 内 `background-image: url(./.images/logo.png);` — 変更する場合は README 指示通りファイル名/パス同期。
- 相対パス前提: 生成時はプロジェクトルートカレントでツールを実行する設計。

## 変更時の注意
- `theme.css` 改変後は再生成が必要。キャッシュは特段扱っていない想定。
- `template.md` を直接編集しても既存出力には影響しない; 新規原稿がその構造を参照。
- Cookiecutter 変数 (`{{cookiecutter.folder_name}}`, `{{cookiecutter.organization}}`, `{{cookiecutter.author}}`) はテンプレート展開時に具体値へ置換される。生成後に生ファイル内へ直接埋め込まれているか確認してから追加変更。

## よくあるタスク例 (エージェント支援)
| 目的 | 手順 (要点) |
|------|-------------|
| 新しいスライド作成 | `input/new.md` を作り front‑matter 省略可 (コマンド側でテンプレート適用想定) / 明示するなら `template.md` をコピー |
| テーマ色変更 | `themes/theme.css` の `background-color` / 線色を編集 |
| ロゴ差替え | `.images/logo.png` を差し替え (名称変えるなら CSS の url を同期) |
| ページ番号書式変更 | `section::after { content: "Page " attr(...); }` を修正 |

## 追加で探すべきファイル (存在前提) が無い場合
`.gemini/` ディレクトリが無い状態ならユーザ環境未初期化。必要なら以下のプレースホルダ生成を提案:
- `.gemini/commands/generate-slides.toml`
- `.gemini/rules/slide_rules.md`
  (README 記述を元に雛形案内)

## 禁止/避ける事項
- 汎用的ベストプラクティスの羅列 (テスト戦略等) — このテンプレートはスライド生成中心。
- 絵文字使用。
- 日本語内の不自然スペース。

## 不確定点の扱い
- Marp CLI 呼び出しコマンド詳細が未掲示: 追加情報が必要な場合だけユーザへ確認し冗長質問は避ける。

以上を基準に、このリポジトリでの自動化/編集提案を行うこと。改善余地や未定義領域があれば差分のみを簡潔に質問してから進める。
