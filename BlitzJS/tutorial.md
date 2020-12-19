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
├── app
│   ├── components
│   │   └── ErrorBoundary.tsx
│   ├── layouts
│   └── pages
│       ├── _app.tsx
│       ├── _document.tsx
│       └── index.tsx
├── db
│   ├── migrations
│   ├── index.ts
│   └── schema.prisma
├── integrations
├── node_modules
├── public
│   ├── favicon.ico
│   └── logo.png
├── utils
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
```

