# Cloud Composer

## 環境の操作

### 環境のアップグレード

#### アップグレード可能なバージョンの確認

- 最新のバージョンにのみアップグレードできる。

```
gcloud beta composer environments list-upgrades ENVIRONMENT_NAME \
    --location asia-northeast1
```

#### アップグレードの実行

- 30分程度掛かる。

```
gcloud beta composer environments update ENVIRONMENT_NAME \
    --location asia-northeast1 --image-version COMPOSER_VERSION
```


## DAG の操作
### DAG の手動実行

```sh
gcloud composer environments run $ENVIRONMENT \
  trigger_dag -- $DAG_NAME \
  --run_id=test$(date "+%Y%m%d%H%M%S") \
  --conf "{ \"execution_date\": \"20210709\" }"
```

- `--run_id` で Run ID を指定できる。
- `--conf` でパラメーターを渡せる。

### DAG 登録

DAG は Cloud Composer が自動的に作成する Cloud Storage のバケットにプレーンなファイルとして保管される。DAG を変更する場合はそのファイルを書き換えるのみでよい。Airflow が定期的に DAG のフォルダ内を読み取って DAG を登録し直すということをしている。

```sh
gcloud composer environments storage dags import \
            --project ${project_id} \
            --environment ${composer_environment_name} \
            --location ${location} \
            --source ./foo.py
# source に指定したファイル/フォルダがそのまま Cloud Storage にアップロードされる
```

### DAG 削除

- Web UI から DAG を削除する場合、即座に DAG は削除されず、なおかつ実行履歴は削除されるために、キャッチアップ実行が走り出すという謎挙動を確認…。
-  [環境内で DAG を削除する](https://cloud.google.com/composer/docs/how-to/using/managing-dags?hl=ja#deleting_a_dag_in_your_environment) => [Airflow ウェブ インターフェースからの DAG の削除](https://cloud.google.com/composer/docs/how-to/using/managing-dags?hl=ja#delete-md) の順で削除を実施するのが良さそう。

```sh
# アップロードされた DAG ファイルの削除
gcloud composer environments storage dags delete \
            --project ${project_id} \
            --environment ${composer_environment_name} \
            --location ${location} \
            foo.py
```

```sh
# メタデータ削除
gcloud composer environments run \
            --project ${project_id} \
            --location ${location} \
            ${composer_environment_name} delete_dag -- ${dag_name}
```

