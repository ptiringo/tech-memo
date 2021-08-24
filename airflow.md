# Airflow

## DAG 作成
DAG に対してコード修正なしに外部から値を注入する場合、以下の2つの手段を取りうる。
- Variable
- Environment Variable

## DAG 実行

### 再実行
- 個々のタスクの実行履歴を Clear することによってそのタスクおよび後続のタスクを再実行することができる。

## UI

### カスタマイズ

#### airflow.cfg

- \[webserver\] navbar_color でナビゲーションバーの色を変更することが可能。


## airflow_db

- Web UI の Data Profiling > Ad HocQuery から Airflow の Database に対してアドホックなクエリを発行できる。

### SQL サンプル

### DAG の実行時間出力

```sql
select
  id,
  dag_id,
  run_id,
  start_date + INTERVAL 9 HOUR as 'start_date (JST)',
  end_date + INTERVAL 9 HOUR as 'end_date (JST)',
  timediff(end_date, start_date) as 'execution_time'
from dag_run
where run_id = 'example_run_id'
order by start_date
```