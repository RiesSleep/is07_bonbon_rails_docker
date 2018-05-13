## Q)docker imageについて

dockerのimageにアクセスする方法とは

要求：前回取得したrubyの2.3.1のイメージの中に入りrubyが本当に入っているのかを確認する

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

## 正解発表

残念。惜しい。
というか私の伝え漏れもあるね。。。
Question01で取得したimageに入り本当にrubyが入っているのかを確認する。

ちなみに
```docker run```
コマンドの他にも既存imageに入る方法があるので探して見るといいよ〜

また後ろの立ち上げるshellについてだけど
/bin/bashではなくbashとかでもok

そしてオプションについての説明
```
-i STDINではなくtarアーカイブファイルから読み込みます
-t 作成がうまくいった場合、作成されたイメージに適用するリポジトリ名
```
