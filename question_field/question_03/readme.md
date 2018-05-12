## Q)docker imageについて

docker imageを削除したい

要求：docekr image一覧を表示しruby:2.3.1のイメージを指定して削除したい

## A)コマンドや回答

```
docker images <- ローカルにあるimageを確認する
docker ps and docker ps -a で現在のコンテナ利用状況を確認する
docker rmi -f ruby:2.3.1  <- 確実に使ってない、もういらなくなったら強制的に消すために -f
$
```
