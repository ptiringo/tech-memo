# gsutil
- Google Cloud 操作用コマンドラインツール `gcloud` とは別に Cloud Storage 操作専用コマンドラインツール `gsutil` が用意されている。

## コマンドサンプル

### gsutil cat

標準出力に指定したオブジェクトの内容を出力する。

```sh
$ gsutil cat gs://sample_bucket/sample.txt
aaaaaaaa
bbbbbbbbbbbb
cccc
```

