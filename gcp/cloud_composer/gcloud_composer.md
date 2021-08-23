## コマンドサンプル

### DAG の手動実行

```sh
gcloud composer environments run $ENVIRONMENT \
  trigger_dag -- $DAG_NAME \
  --run_id=test$(date "+%Y%m%d%H%M%S") \
  --conf "{ \"execution_date\": \"20210709\" }"
```

- `--run_id` で Run ID を指定できる。
- `--conf` でパラメーターを渡せる。