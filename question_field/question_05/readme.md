## Q)docker-compose.ymlについて

docker-compose.ymlの基本的な構成は以下の通りである

```
version: '3'
services:
  app:
    container_name: is_ruby
    build:
      context: .
      dockerfile: ./docker/ruby/Dockerfile
    environment:
      MYSQL_DATABASE: db_test
      MYSQL_USER: db_test
      MYSQL_PASSWORD: db_test
      MYSQL_ROOT_PASSWORD: db_test
    command: bundle exec rails s -p 3000 -b '0.0.0.0'
    volumes:
      - .:/rails_app
      - ./public:/rails_app/public
      - ./tmp:/rails_app/tmp
      - ./log:/rails_app/log
    depends_on:
      - db
    stdin_open: true
    tty: true
    ports:
      - ${HTTP_PORT}:3000
# MySQL Setting
  db:
    container_name: is_mysql
    build:
      context: .
      dockerfile: ./docker/mysql/Dockerfile
    environment:
      MYSQL_DATABASE: db_test
      MYSQL_USER: db_test
      MYSQL_PASSWORD: db_test
      MYSQL_ROOT_PASSWORD: db_test
    volumes:
      - db-data:/var/lib/mysql
    ports:
      - ${DB_PORT}:3306
volumes:
  db-data:
```

要求：以下のオプションについて回答解説せよ


- build:
- container_name:
- context:
- dockerfile:
- volumes:
- command:
- depends_on:
- ports:
- image:


## A)コマンドや回答
