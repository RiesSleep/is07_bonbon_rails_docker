## Q)docker imageについて

dockerのimageにアクセスする方法とは

要求：rubyの2.3.1のイメージの中に入りrubyが本当に入っているのかを確認する

## A)コマンドや回答

```
docker run --name tuna_ruby -it ruby:2.3.1 /bin/bash
```

Rubyのバージョンの確認
```
root@7a7a9d66f66c:/# ruby --version
ruby 2.3.1p112 (2016-04-26 revision 54768) [x86_64-linux]
$
```
