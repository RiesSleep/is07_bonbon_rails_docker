## Q)docker-composeでのアプリケーション立ち上げについて

### 事前準備

```
$ cd question_field/question_final/docker_for_rails
```

このディレクトリにて
アプリケーションの立ち上げを行うとエラーが発生する

要求：そのエラーの内容とトラブルシューティングを行い、`Yah You're on Rails!`の画面を表示しなさい

参考
```
## 1st
$ docker-compose run --rm app rails new . --force --database=mysql --skip-bundle

## 2st
$ sudo chown -R $USER:$USER .

## 3st
db設定変更

## 4st
mysql user権限付与

## 5st
dbのcreateとmigrate
```

## A)解決までのメモやコマンド

```
$
```
