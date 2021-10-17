# 設計するときの分割(疎結合)について考えてみるといいかも？

## 疎結合とは？

「システムを構成する要素が依存していない」ことです。
別のものに差し替えたときに影響がないってことで判断できると思います。

（例：MySQL→Postgress に移行するとか）

## 外部要因がどれだけあるか考える

外部要因を考えるときは、「アプリ作るときに、自分で作らずにお願いするところ」って言っても良いかも

例えば、パッと思いつくのは、DBとかでしょうか

## DBだけでよいのか？

考え出すと実は結構あります

ほぼ必須になるだけでも以下

- DB
- ライブラリ
- HTTP

構成によっては

- 各SaaS
- コマンドラインインターフェース
- スケジューラー(ジョブマネージャー)
- メールサーバー

## 外部と疎結合にするには

竹内のコツとしては、外部要因ごとにインターフェースを作成します。

イメージとしては、外部要因の数だけ形にあったコンセントを生やすイメージ。

## HTTPで考えてみると

HTTPでやりとりするAPIを例に出してみます。

インターフェースなので、入り口と出口があります。
なのでコンセントの穴を作りましょう。

そしてどんな形でもよいわけではありません。
HTTPの形に合わせたコンセントの形状にする必要があります。

なので必要なこととしては以下になります。

- 入り口を作る
- 出口を作る
- 形状に合わせる

### コードにしてみよう

試しにコードにしてみましょう。

``` typescript
// サンプルモデル
SampleModel {
  id: number;
  name: string;
}


// 入り口
SampleAPIHTTPRequest {
  method: string; // HTTPメソッド(GETとか)
  body: SampleModel;
  status: number;
}

// 出口
SampleAPIHTTPResponse {
  status：number
  body: SampleModel;
}
```

この状態だと、アプリのモデルとHTTPが密接な関係なっちゃってます。 なのでもうちょっと分割しましょう。

``` typescript
// 入り口
SampleAPIRequest {
  id:number;
  name:string;
}

// 出口
SampleAPIResponse {
  id:number;
  name:string;
}

```

でもHTTPはGET、POSTでコンセントの形が違いますよね？ もう少し分けてみましょう。

``` typescript
// 入り口(POST)
SampleAPICreateRequest {
  name:string;
}

// 出口(POST)
SampleAPICreateResponse {
  id:number;
}

// 入り口(GET)
SampleAPIGetRequest {
  id:number;
}

// 出口 (GET)
SampleAPIGetResponse {
  id:number;
  name:string;
}

// PUT、DELETEも形に合わせてつくる
・・・
```

これで、インターフェース（コンセント）ができました！

## コンセントを作ったら？

僕たちが使うアプリで使うモデルとインターフェースのモデルを、変換しましょう。

変換後のモデルでビジネスロジックに持っていくことで
ビジネスロジックと、HTTPインターフェースが完全に切り離された状態になります。

## まとめ

外部要因に合わせたインターフェース(コンセント)を作ることで、アプリケーションと切り離せることができるので、
インターフェースの修正だけで、アプリケーション(ビジネスロジック)を修正する必要がなくなり、疎結合と言われる状態にすることができるよ！
