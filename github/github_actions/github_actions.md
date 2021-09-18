# GitHub Actions

## 用語

- ワークフロー
  - YAMLファイルで構成される自動化プロセス。
  - 1つのYAMLファイルから1つのワークフローが構成される。
- ジョブ
  - ワークフローは1つ以上のジョブから構成される。
  - ジョブはデフォルトで並列で実行される。
- ステップ
  - ジョブは1つ以上のステップから構成される。
  - ステップは順番に実行される。
- アクション
  - 再利用可能なタスク。
  - アクションはステップとして実行可能。

## YAML ファイルの書き方

```yaml
# ワークフロー名
name: example-workflow

# ワークフローの実行の引き金となるイベント
# https://docs.github.com/en/actions/reference/events-that-trigger-workflows
on: workflow_dispatch

# ワークフローの全てのジョブとステップで利用可能な環境変数
env:
  EXAMPLE_ENVIRONMENT_VALUE: example

# ジョブ定義
jobs:

  # ジョブID
  example-job:

    # ジョブを実行するマシンタイプ
    runs-on: ubuntu-latest

    # ステップ定義
    steps:

      - name: Checkout              # ステップ名
        uses: actions/checkout@v2   # アクションの指定

      - name: Set up JDK 11         # ステップ名
        uses: actions/setup-java@v2 # アクションの指定
        with:                       # アクションで定義されたインプットパラメーター
          java-version: "11"
          distribution: "adopt"

      - name: Display Java version  # ステップ名
        run: java --version         # OS のシェルで実行されるコマンドラインプログラム

  # ジョブID
  another-example-job:

    # ジョブを実行するマシンタイプ
    runs-on: ubuntu-latest

    # ステップ定義
    steps:

      - name: Echo                   # ステップ名
        run: echo Hello              # OS のシェルで実行されるコマンドラインプログラム
```

### アクション
- actions/cache
  - 依存ライブラリ等のキャッシュ
- actions/setup-java
  - Java のインストール
- google-github-actions/setup-gcloud
  - gcloud のインストール