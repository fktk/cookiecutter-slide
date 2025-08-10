# プレゼンテーション資料 (`{{cookiecutter.folder_name}}`)

このディレクトリは、プレゼンテーションスライドの作成に必要なファイルを管理するためのものです。

## スライド生成の手順

### 1. ロゴの準備

-   `.images/` ディレクトリに、スライドに表示したいロゴ画像を配置します。
-   デフォルトでは `logo_primary.png` という名前の画像が参照されます。必要に応じて `themes/theme.css` 内のファイル名を変更してください。

### 2. スライド原稿の作成

-   `input/` ディレクトリに、スライドの内容を記述したMarkdownファイルを作成します。
-   ファイル名は任意です（例: `draft.md`）。

### 3. スライドの生成

-   以下のGemini CLIコマンドを実行して、MarkdownからPDFスライドを生成します。

    ```bash
    gemini -c .gemini/commands/generate-slides.md input/your-markdown-file.md
    ```
    ※ `input/your-markdown-file.md` は、ステップ2で作成したファイルへのパスに置き換えてください。

-   `generate-slides.md`コマンドは、以下の処理を自動的に行います。
    1.  入力されたMarkdownファイルを読み込む。
    2.  `.gemini/rules/slide_rules.md` のルールに基づき、内容をスライド形式に最適化する。
    3.  `themes/theme.css` で定義されたデザインを適用する。
    4.  Marp CLIを使用してPDFに変換し、`output/` ディレクトリに保存する。

### 4. 生成物の確認

-   `output/` ディレクトリに、生成されたPDFファイルが格納されています。

## カスタマイズ

-   スライドのデザイン（色、フォント、レイアウトなど）は `themes/theme.css` を編集することでカスタマイズできます。
