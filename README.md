# Cookiecutter Slide Generator

AIを活用したMarpスライド生成のためのプロジェクトテンプレートです。

## 概要

このCookiecutterテンプレートは、Markdownの原稿からAI（Google GeminiやGitHub Copilot）と[Marp](https://marp.app/)を利用して、プレゼンテーションスライドを効率的に作成するためのプロジェクト構造を迅速にセットアップします。

単なる雛形だけでなく、AIへの指示（プロンプト）や定型的な変換処理を組み込んだ、実践的なワークフローを提供します。

### 特徴

-   **構造化されたディレクトリ**: 原稿、ルール、中間生成物、最終成果物などを体系的に管理できます。
-   **AI連携**: Gemini CLIやGitHub Copilotのカスタムコマンドと連携し、原稿の要約やスライド形式への変換を半自動化します。
-   **カスタマイズ可能**: スライドのテーマやテンプレートは簡単に変更できます。

## 前提条件

このテンプレートを最大限に活用するには、以下のツールのインストールが必要です。

-   [Cookiecutter](https://cookiecutter.readthedocs.io/en/stable/): テンプレートからプロジェクトを生成します。
-   [Marp CLI](https://github.com/marp-team/marp-cli): Markdownからスライド（PDF, HTML）を生成します。
-   [Google Gemini CLI](https://github.com/google/generative-ai-cli) (推奨): 原稿の整形やスライド化に利用します。
-   [GitHub Copilot](https://github.com/features/copilot) (推奨): 同様にAI連携に利用できます。

## 使い方

1.  ターミナルで以下のコマンドを実行し、テンプレートからプロジェクトを生成します。

    ```bash
    cookiecutter gh:fktk/cookiecutter-slide
    ```

2.  プロンプトに従って、プロジェクト名（フォルダ名）などを入力します。

    ```
    folder_name [20250810_butyohokoku]: my-presentation
    author [TK]: Your Name
    organization [TK]: Your Organization
    ```

3.  入力したプロジェクト名（例: `my-presentation`）でディレクトリが作成されます。

## 生成されるプロジェクト

生成されたディレクトリに移動し、その中の`README.md`や`GEMINI.md`に従ってスライド作成を開始してください。

基本的なフローは以下の通りです。

1.  `input/`ディレクトリにMarkdownで原稿を作成します。
2.  Gemini CLIやCopilotのカスタムコマンドを実行し、`rules/`内のルールに基づいて原稿を整形し、`artifact/`に中間ファイルを生成します。
3.  中間ファイルを`template.md`と組み合わせて、スライド用のMarkdownを生成します。
4.  Marp CLIで最終的なスライド（PDFなど）を`output/`ディレクトリに出力します。

詳細な手順やカスタマイズ方法は、生成されたプロジェクト内のドキュメントを参照してください。
