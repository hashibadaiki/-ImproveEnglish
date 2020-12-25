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

## 最初のページを書くで

開発環境（「プロジェクト」）がセットアップされたので、アプリの構築を開始する準備が整いました。
まず、最初のページを作成します。 ファイルapp / pages / index.tsxを開き、次のコードをその中に入れます。

```js
const Index = () => (
  <div>
    <h1>Hello, world!</h1>
  </div>
)
export default Index
```

blitzで一番シンプルなページです。
ブラウザに戻って、http://localhost:3000 を訪れてみたください。
あなたのテキストが表示されるはずです。index.tsxファイルを編集してみてください。
これが確認できたら、次のセクションに進みましょう。

## コンテンツを生成する

Blitzは、ボイラープレートコードをスキャフォールディングするためのgenerateと呼ばれる便利なコマンドを提供しています。

ここでは、generateを使って2つのモデルを作成します。QuestionとChoiceです。
質問には質問のテキストと選択肢のリストがあります。選択肢には、選択肢のテキスト、投票数、関連する質問があります。
どちらのモデルも自動的にid、作成タイムスタンプ、最終更新タイムスタンプを持っています。

最初に、質問モデルに関連するすべてのものを生成します。

```js
blitz generate all question text:string choices:choice[]
✔ Model for 'question' created successfully:
> model Question {
>   id        Int      @default(autoincrement()) @id
>   createdAt DateTime @default(now())
>   updatedAt DateTime @updatedAt
>   text      String
>   choices   Choice[]
> }
Now run blitz db migrate to add this model to your database
CREATE    app/questions/pages/questions/index.tsx
CREATE    app/questions/pages/questions/new.tsx
CREATE    app/questions/pages/questions/[questionId]/edit.tsx
CREATE    app/questions/pages/questions/[questionId].tsx
CREATE    app/questions/components/QuestionForm.tsx
CREATE    app/questions/queries/getQuestions.ts
CREATE    app/questions/queries/getQuestion.ts
CREATE    app/questions/mutations/createQuestion.ts
CREATE    app/questions/mutations/deleteQuestion.ts
CREATE    app/questions/mutations/updateQuestion.ts
```

次に、対応するクエリとミューテーションを使用してChoiceモデルを生成します。
Choiceモデルのページを生成する必要がないため、今回はある種のリソースを渡します。

`blitz generate resource choice text votes:int:default[0] belongsTo:question
`

>注：端末でzshを使用する場合、正しく解釈されるように、フィールドをデフォルト値で引用符（ ""）で囲む必要があります。このように： "votes：int：default [0]"

```
✔ Model for 'choice' created successfully:
> model Choice {
>   id         Int      @default(autoincrement()) @id
>   createdAt  DateTime @default(now())
>   updatedAt  DateTime @updatedAt
>   text       String
>   votes      Int      @default(0)
>   question   Question @relation(fields: [questionId], references: [id])
>   questionId Int
> }
Now run blitz db migrate to add this model to your database
CREATE    app/choices/queries/getChoices.ts
CREATE    app/choices/queries/getChoice.ts
CREATE    app/choices/mutations/createChoice.ts
CREATE    app/choices/mutations/deleteChoice.ts
CREATE    app/choices/mutations/updateChoice.ts
```

>注：変更が必要な場合でかつ、generate以外を使用する場合、必要に応じてdb /schema.prismaファイルを直接編集することもできます。


次に、データベースを移行する必要があります。
これは、スキーマを何らかの方法で編集したことを伝える方法です。
以下のコマンドを実行します。移行名の入力を求められたら、任意の名前を入力できます（一般的には「init db」）

`blitz db migrate`

## APIを使ってみよう！

インタラクティブなblitz shellを使っていきましょう。
blitz consoleを呼び出すのは `blitz console`でOK

 

