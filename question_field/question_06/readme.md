## Q)docker-compose upについて

基本的なdocker-compose.ymlは以下の通りである

```
version: '3'
services:
  db:
    image: mysql:5.7.21
    container_name: mysql

    environment:
      MYSQL_DATABASE: db_test
      MYSQL_USER: db_test
      MYSQL_PASSWORD: db_test
      MYSQL_ROOT_PASSWORD: db_test

    volumes:
         - db-data:/var/lib/mysql
    ports:
      - "3306:3306"
volumes:
  db-data:

```





要求：
- container_nameを記載すること
- imageのバージョンを5.7.21に指定すること
- environmentを記載すること
- volumesを利用し永続化すること
- docker-compose.ymlからdockerを立ち上げプロセスの確認とコンテナ内に入って見ること
- mysqlのバージョンを確認すること

## A)コマンドや回答

```
version: '3'
services:
  db:
    image: mysql:5.7.21
    container_name: mysql

    environment:
      MYSQL_DATABASE: db_test
      MYSQL_USER: db_test
      MYSQL_PASSWORD: db_test
      MYSQL_ROOT_PASSWORD: db_test

    volumes:
         - db-data:/var/lib/mysql
    ports:
      - "3306:3306"
volumes:
  db-data:

```
## mysqlコンテナ内に入る
```
~/D/g/is07_mayo_rails_docker   -  docker ps                           2018年05月18日 17時27分50秒
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                     NAMES
55801a5a3640        mysql:5.7.21        "docker-entrypoint.s…"   5 minutes ago       Up 15 seconds       0.0.0.0:3306->3306/tcp    mysql
367ccb67ecd6        mysql               "docker-entrypoint.s…"   12 days ago         Up 2 days           0.0.0.0:13306->3306/tcp   lara-mysql
 ~/D/g/is07_mayo_rails_docker   -  docker exec -it mysql bash    
```
## コンテナ内でmysqlのバージョン確認
```
root@55801a5a3640:/# mysql --version
mysql  Ver 14.14 Distrib 5.7.21, for Linux (x86_64) using  EditLine wrapper
```
