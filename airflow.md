# Airflow

## UI

### カスタマイズ

#### airflow.cfg

- \[webserver\] navbar_color でナビゲーションバーの色を変更することが可能。


## SQL サンプル

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