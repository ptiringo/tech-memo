# avro-tools とは
- Avro 形式のファイルを扱うための公式のコマンドラインツール

# インストール

## Mac (Homebrew)
```
brew install avro-tools
```

あるいは https://avro.apache.org/releases.html からダウンロード。

# 利用法確認

```
$ avro-tools
Version 1.10.1 of Apache Avro
Copyright 2010-2015 The Apache Software Foundation

This product includes software developed at
The Apache Software Foundation (https://www.apache.org/).
----------------
Available tools:
    canonical  Converts an Avro Schema to its canonical form
          cat  Extracts samples from files
      compile  Generates Java code for the given schema.
...
```

jar ファイルを直接ダウンロードした場合は

```
$ java -jar avro-tools-x.xx.x.jar
Version 1.10.1 of Apache Avro
Copyright 2010-2015 The Apache Software Foundation

This product includes software developed at
The Apache Software Foundation (https://www.apache.org/).
----------------
Available tools:
    canonical  Converts an Avro Schema to its canonical form
          cat  Extracts samples from files
      compile  Generates Java code for the given schema.
...
```

※以後、コマンド実行方式は Homebrew を使ってインストールした方式で記載。

# よく使うコマンド

## Avro ファイルの内容の出力

### JSON 出力

avro のデータの内容を JSON に変換して標準出力に出力します。

```
avro-tools tojson sample.avro
```

標準入力から受け付けることもできる。

```
cat sample.avro | avro-tools tojson -
```

## レコード数のカウント

```
avro-tools count sample.avro
```

## Avro の作成

```
avro-tools fromjson sample.json --schema-file sample_schema.json > sample.avro
```

## スキーマ情報の取得

```
avro-tools getschema sample.avro
```