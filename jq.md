### コマンドサンプル

#### 特定のフィールドのみを抽出

```sh
cat example.json | jq '{ .field_a: .field_a, field_b: .field_b }'
```

#### フィルター

```sh
cat example.json | jq 'select(.field_a == "aaa")'

# and 条件
cat example.json | jq 'select(.field_a == "aaa" and .field_b == "bbb")'
```