[翻訳元](https://blitzjs.com/docs/tutorial)

# BlitzJS

Reactのフルスタックフレームワーク
公式Docsを翻訳する

注意書きの内容は一緒。アルファ版だからね〜

Blitzを試してくれてありがとう！投票アプリを今回は作っていくよ。

Blitzがすでにインストールされていることを前提としています。
ターミナルで次のコマンドを実行すると、Blitzがインストールされているかどうか、および使用しているバージョンを確認できます

`blitz -v`

Blitzがインストールされている場合は、インストールのバージョンが表示されます。
そうでない場合は、「コマンドが見つかりません」などのエラーが表示されます。

Blitzを初めて使用する場合は、初期設定から始める必要があります。
これらすべてを処理するコマンドを提供し、開始するために必要な構成とコードを生成します。

コマンドラインから、コードを保存するディレクトリにcdして、次のコマンドを実行します。

`blitz new mysite`

これでそのディレクトリに `my site` というディレクトリ を作りました

さぁ、 `blitz new` で何が作れたか見ていきましょう

```
mysite
// appは多くの場合container_dirです。
//  pagesかAPIルーターが入っています。
├── app
│   ├── components
│   │   └── ErrorBoundary.tsx
│   ├── layouts
│   └── pages
│       ├── _app.tsx
│       ├── _document.tsx
│       └── index.tsx
// dbは、データベース構成が行われる場所です。
// モデルを作成したり、migrationを確認したりする場合は、ここにアクセスしてください。
├── db
│   ├── migrations
│   ├── index.ts
│   └── schema.prisma
// 省略
├── integrations
// 省略
├── node_modules
// 静的なファイル置き場
├── public
│   ├── favicon.ico
│   └── logo.png
// utilityなファイルの置き場
├── utils
// 以下省略
├── .babelrc.js
├── .env
├── .eslintrc.js
├── .gitignore
├── .npmrc
├── .prettierignore
├── README.md
├── blitz.config.js
├── package.json
├── tsconfig.json
└── yarn.lock

省略は他FWと大体同一
```

## DevServerについて

じゃあblitzがどんなふうに動くか見てみましょう！
`mysite` dirにいることを確認して `blitz start` を入力してください。

CLに次の出力が表示されます。

〜〜

これでサーバーが動いています。local:3000に行ってみてください。blitzのロゴが出てるでしょ？！
無事に動いてますね＾＾


