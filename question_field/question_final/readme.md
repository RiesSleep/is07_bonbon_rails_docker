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

# 1回目のエラー
```
$ docker-compose run --rm app rails new . --force --database=mysql --skip-bundle

```
何も設定しないででたエラー
```
Step 7/9 : RUN bundle install
 ---> Running in 5c20ecf29439
Could not locate Gemfile
ERROR: Service 'app' failed to build: The command '/bin/sh -c bundle install' returned a non-zero code: 10
>
```
## RubyのDockerfileを修正
Gemfileが見つからねーよって怒られてますね・・・
rubyのDokerfileが読み込まれるときに怒られてる

```
> cat Dockerfile                                                          2018年05月18日 17時59分46秒
FROM ruby:2.5.1
LABEL  maintainer "k-waragai <kazuxtuna@gmail.com>"

# Initial command
RUN apt-get update -qq && \
    apt-get install -y build-essential libpq-dev nodejs

# WORKDIR ENV
ENV work_dir /rails_app

# Rails setting
RUN mkdir ${work_dir}
WORKDIR ${work_dir}

メモ:Gemfileがナーイ
追加:
COPY ./Gemfile /${work_dir}/Gemfile
COPY ./Gemfile /${work_dir}/Gemfile.lock

RUN bundle install

# sockets dir setting
RUN mkdir -p ${work_dir}/tmp/sockets

COPY . ${work_dir}
>                        
```
## Mysqlの設定
作成したmysqlコンテナに入る
#docker exec -it is_mysql bash

> バージョンの確認
```
root@de2cac98f4b5:/# mysql --version
mysql  Ver 14.14 Distrib 5.7.21, for Linux (x86_64) using  EditLine wrapper
```

> 設定　
```
mysql> GRANT ALL PRIVILEGES ON *.* TO 'db_test'@'%';
Query OK, 0 rows affected (0.00 sec)
```

# 2回目のエラー

```
docker-compose run --rm app rails db:create db:migrate
Starting is_mysql ... done
Usage:
  rails new APP_PATH [options]

Options:
      [--skip-namespace], [--no-skip-namespace]            # Skip namespace (affects only isolated applications)
  -r, [--ruby=PATH]                                        # Path to the Ruby binary of your choice
                                                           # Default: /usr/local/bin/ruby
  -m, [--template=TEMPLATE]                                # Path to some application template (can be a filesystem path or URL)
  -d, [--database=DATABASE]                                # Preconfigure for selected database (options: mysql/postgresql/sqlite3/oracle/frontbase/ibm_db/sqlserver/jdbcmysql/jdbcsqlite3/jdbcpostgresql/jdbc)
                                                           # Default: sqlite3
      [--skip-yarn], [--no-skip-yarn]                      # Don't use Yarn for managing JavaScript dependencies
      [--skip-gemfile], [--no-skip-gemfile]                # Don't create a Gemfile
  -G, [--skip-git], [--no-skip-git]                        # Skip .gitignore file
      [--skip-keeps], [--no-skip-keeps]                    # Skip source control .keep files
  -M, [--skip-action-mailer], [--no-skip-action-mailer]    # Skip Action Mailer files
  -O, [--skip-active-record], [--no-skip-active-record]    # Skip Active Record files
      [--skip-active-storage], [--no-skip-active-storage]  # Skip Active Storage files
  -P, [--skip-puma], [--no-skip-puma]                      # Skip Puma related files
  -C, [--skip-action-cable], [--no-skip-action-cable]      # Skip Action Cable files
  -S, [--skip-sprockets], [--no-skip-sprockets]            # Skip Sprockets files
      [--skip-spring], [--no-skip-spring]                  # Don't install Spring application preloader
      [--skip-listen], [--no-skip-listen]                  # Don't generate configuration that depends on the listen gem
      [--skip-coffee], [--no-skip-coffee]                  # Don't use CoffeeScript
  -J, [--skip-javascript], [--no-skip-javascript]          # Skip JavaScript files
      [--skip-turbolinks], [--no-skip-turbolinks]          # Skip turbolinks gem
  -T, [--skip-test], [--no-skip-test]                      # Skip test files
      [--skip-system-test], [--no-skip-system-test]        # Skip system test files
      [--skip-bootsnap], [--no-skip-bootsnap]              # Skip bootsnap gem
      [--dev], [--no-dev]                                  # Setup the application with Gemfile pointing to your Rails checkout
      [--edge], [--no-edge]                                # Setup the application with Gemfile pointing to Rails repository
      [--rc=RC]                                            # Path to file containing extra configuration options for rails command
      [--no-rc], [--no-no-rc]                              # Skip loading of extra configuration options from .railsrc file
      [--api], [--no-api]                                  # Preconfigure smaller stack for API only apps
  -B, [--skip-bundle], [--no-skip-bundle]                  # Don't run bundle install
      [--webpack=WEBPACK]                                  # Preconfigure for app-like JavaScript with Webpack (options: react/vue/angular/elm/stimulus)

Runtime options:
  -f, [--force]                    # Overwrite files that already exist
  -p, [--pretend], [--no-pretend]  # Run but do not make any changes
  -q, [--quiet], [--no-quiet]      # Suppress status output
  -s, [--skip], [--no-skip]        # Skip files that already exist

Rails options:
  -h, [--help], [--no-help]        # Show this help message and quit
  -v, [--version], [--no-version]  # Show Rails version number and quit

Description:
    The 'rails new' command creates a new Rails application with a default
    directory structure and configuration at the path you specify.

    You can specify extra command-line arguments to be used every time
    'rails new' runs in the .railsrc configuration file in your home directory.

    Note that the arguments specified in the .railsrc file don't affect the
    defaults values shown above in this help message.

Example:
    rails new ~/Code/Ruby/weblog

    This generates a skeletal Rails installation in ~/Code/Ruby/weblog.

```
# 3回目のエラー
database.ymlでhostをlocalhostで指定してた


```
