## Q)docker-compose upについて

基本的なdocker-compose.ymlは以下の通りである

```
version: '3'
services:
  db:
    image: mysql
    ports:
      - "3306:3306"
```

要求：
- container_nameを記載すること
- imageのバージョンを5.7.21に指定すること
- environmentを記載すること
- volumesを利用し永続化すること
- docker-compose.ymlからdockerを立ち上げプロセスの確認とコンテナ内に入って見ること
- mysqlのバージョンを確認すること

## A)コマンドや回答
