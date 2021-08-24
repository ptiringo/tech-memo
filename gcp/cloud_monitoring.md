### Terraform によるダッシュボード作成
- Cloud Monitoring のダッシュボードは定義ファイル (JSON) から作成することができる。
  - https://cloud.google.com/blog/products/management-tools/cloud-monitoring-dashboards-using-an-api
  - gcloud コマンドから作成する場合は JSON ではなくて YAML ファイルでもいけそう。
- 既存のダッシュボード定義をエクスポートすることも可能。
  `gcloud monitoring dashboards describe $DASHBOARD_ID --format json`
