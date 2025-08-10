# Cookiecutter Slide Generator

これは、Gemini CLIとMarpを使用してプレゼンテーションスライドを生成するためのプロジェクト構造を迅速にセットアップするCookiecutterテンプレートです。

## 目的

このテンプレートは、スライド作成における定型的な作業を自動化し、コンテンツ作成に集中できる環境を提供します。以下の特徴があります。

-   **構造化されたディレクトリ**: 入力、出力、テーマ、画像などのファイルが整理されています。
-   **Gemini CLI連携**: Geminiへの指示（プロンプト）が事前定義されており、コマンド一つでスライドを生成できます。
-   **MarpによるPDF出力**: Markdownから美しいデザインのPDFスライドを生成します。

## 前提条件

このテンプレートを使用するには、以下のツールがインストールされている必要があります。

-   [Cookiecutter](https://cookiecutter.readthedocs.io/en/stable/installation.html)
-   [Google Gemini CLI](https://github.com/google/generative-ai-cli)
-   [Marp CLI](https://github.com/marp-team/marp-cli)

## 使い方

1.  ターミナルで以下のコマンドを実行します。

    ```bash
    cookiecutter gh:fktk/cookiecutter_slide
    ```

2.  プロンプトに従って、プロジェクト名（フォルダ名）を入力します。

    ```
    folder_name [20250810]: my-presentation
    ```

3.  `my-presentation`という名前のディレクトリが作成されます。

## 生成されるプロジェクト

生成されたディレクトリに移動し、その中の`README.md`に従ってスライド作成を開始してください。
