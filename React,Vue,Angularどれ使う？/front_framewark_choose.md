# React,Vue,Angularどれ使う？

結論
React最強。でも時と場合によるよ

## React

フレームワークというよりJavascriptライブラリでございます。
ほかのフレームワークと比べてビルドシステムが超シンプル
-> 一番JavaScriptに近いです。

### Reactのメリット

- Javascriptとほぼ同じ、実質ライブラリなので。
- 既存のパッケージ等をそのまま使用できることが多い
- シンプルが故に軽い

### Reactのデメリット

- エコシステム周りを構築するのが大変
  - webpackのそこそこ知識が要求される。
- React側でやってくれることが少ない。

## Vue

HTMLの部分とJavascriptのロジック部分をまとめて1コンポーネントにできる。
フレームワークの部分でやってくれることが多く、適当に書いてもパフォーマンス結構良い。
-> Vue独自のビルドシステムが存在する（.vueファイルが必要になる）

### Vueのメリット

- 一つのファイルに、ロジック、スタイル(HTML)を分けた状態でありつつ1オブジェクトとして管理できる。
- 実装者が深く考えなくても、パフォーマンスが良い。

### Vueのデメリット

- Vue独自のディレクティブを覚えなくちゃいけない。
- 独自のビルドシステムを持っているので、ライブラリ使えるかわからん。
- 色々やってくれるから重い

## Angular

ゴリゴリのフレームワーク。
ファイルの置き方から全て指定通りにやる必要がある。
-> Angularを使ってさえいればどの現場でも設計はおなじになる。

### Angularのメリット

- 設計が必ずおなじになる。（フォルダ構成とか）
  - どこに何があるかとてもわかり易い。
- 実装者が深く考えなくても、パフォーマンスが良い。（Vueより強い）

### Angularのデメリット

- 独自のビルドシステムを持っているので、ライブラリ使えるかわからん。（Vueよりやばい）
- 色々やってくれるから重い（Vueより重い）
- ファイルがめちゃくちゃ多くなる。
- 自分たちの設計を介入させる余地がない。

## どういった現場に向いてるか？

### Reactが向いてる現場

- Javascript、Webpackに詳しい人材がいる。
- 静的型付け出身の人が多い。
- ガチ勢が多い。
- 長生きしそうなシステム。

### Vueが向いてる現場

- マークアップエンジニア出身が多い
- 動的型付け出身の人が多い。？？？
  - 最近はコンポジットAPIとやらが出てきて、TypeScriptが違和感なくかけてきてるらしい。
- レンダリング周りの知識を有している人がいない。

### Angularが向いてる現場

- お堅い現場。
- Googleが好きな人が多い。

## 竹内は何を選ぶか？

Reactを使いたい。

なぜか？

- Javascriptに近いので、新規で覚えることも少ない。
- 新たなライブラリが出ても、ほぼ確実に動く。
- 軽いからコンテナも軽くなる。
- うしろだてがFacebook。
- 世界で見ると使用している会社が多いので、フロントでゲームチェンジャーな技術が出てきてもReactにしか対応していないパターンが多くなりそう。（Next.jsとかがまさにそれ）

上記4点で安心感がある。
