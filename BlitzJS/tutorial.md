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

consoleが表示されたらAPI叩いて遊んでみてね。

## generate コンテンツの修正

※アプリを再度実行する前に、生成されたコンテンツの一部をカスタマイズする必要があります。
最終的には、これらの修正は必要ありませんが、今のところ、いくつかの未解決の問題を回避する必要があります。 

### deleteQuestion mutation

Prismaはまだ「カスケード削除」をサポートしていません。
このチュートリアルのコンテキストでは、現在のところ、質問を削除する際に選択肢データを削除しないことを意味します。
これを手動で行うには、生成された deleteQuestion mutationを一時的に増強する必要があります。
テキストエディタで app/questions/mutations/deleteQuestion.ts を開き、関数本体の先頭に以下を追加してください。

追加するとこんな感じ

```
export default async function deleteQuestion({where}: DeleteQuestionInput, ctx: Ctx) {
  ctx.session.authorize()
  // TODO: remove once Prisma supports cascading deletes
  await db.choice.deleteMany({where: {question: {id: where.id}}})
  const question = await db.question.delete({where})
  return question
}
```

このミューテーションは、質問自体を削除する前に、質問に関連付けられた選択肢を削除するようになりました。

### Question pages

今の状態だと使えないので修正していこー！
(generateで定義したモデルを使っていない)
 
 QuestionListが生成されていることに注意してください。

`<a>{question.name}</a>`

上で書いた通りnameというフィールドは作っていない為、このままではエラーが出ます。

`question.text`　という風に置き換えてください。

```
export const QuestionsList = () => {
  const [questions] = useQuery(getQuestions, {orderBy: {id: "desc"}})
  return (
    <ul>
      {questions.map((question) => (
        <li key={question.id}>
          <Link href="/questions/[questionId]" as={`/questions/${question.id}`}>
            <a>{question.text}</a> 
          </Link>
        </li>
      ))}
    </ul>
  )
}
```

次に同様の理由で `new.tsx` のフォームを修正しましょう。

```
// 修正前
const question = await createQuestionMutation({data: {name: "MyName"}})

// 修正後
const question = await createQuestionMutation({
  data: {text: "Do you love Blitz?", choices: {create: [{text: "Yes!"}]}},
})
```

最後に `edit.tsx` も修正します。

```
// 修正前
const updated = await updateQuestionMutation({
  where: {id: question.id},
  data: {text: "Do you really love Blitz?"},
})

// 修正後
const updated = await updateQuestionMutation({
  where: {id: question.id},
  data: {name: "MyNewName"},
})
```

素晴らしい！これで `blitz start` を打ち込んで `localhost3000` に行ってみてください。

## 最小限のフォームを書く

これまでのところとても順調です！
次に行うことはフォームに実際の値を入力することです。
現時点では全ての質問に、同じ名前が付けられています。
QuestionForm.tsxを確認してください。

div で括られた部分を下記の内容に置き換えてください。

```
<input placeholder="Name" />
<input placeholder="Choice 1" />
<input placeholder="Choice 2" />
<input placeholder="Choice 3" />
```

最後に全てのデータが送信されていることについて確認します。
new.tsx を開いて置き換えます。

```
import {Head, Link, useRouter, BlitzPage} from "blitz"
import createQuestion from "app/questions/mutations/createQuestion"
import QuestionForm from "app/questions/components/QuestionForm"
const NewQuestionPage: BlitzPage = () => {
  const router = useRouter()
  const [createQuestionMutation] = useMutation(createQuestion)
  return (
    <div>
      <Head>
        <title>New Question</title>
        <link rel="icon" href="/favicon.ico" />
      </Head>
      <main>
        <h1>Create New Question </h1>
        <QuestionForm
          initialValues={{}}
          onSubmit={async (event) => {
            try {
              const question = await createQuestionMutation({
                data: {
                  text: event.target[0].value,
                  choices: {
                    create: [
                      {text: event.target[1].value},
                      {text: event.target[2].value},
                      {text: event.target[3].value},
                    ],
                  },
                },
              })
              alert("Success!" + JSON.stringify(question))
              router.push("/questions/[questionId]", `/questions/${question.id}`)
            } catch (error) {
              alert("Error creating question " + JSON.stringify(error, null, 2))
            }
          }}
        />
        <p>
          <Link href="/questions">
            <a>Questions</a>
          </Link>
        </p>
      </main>
    </div>
  )
}
export default NewQuestionPage
```

## 質問のリスト

一息つく時間です。ブラウザの http://localhost:3000/questions に戻って、あなたが作成したすべての問題を見てください。
ここに質問の選択肢をリストアップするのはどうでしょうか? 
まず、質問のクエリをカスタマイズする必要があります。
Prismaでは、ネストされたリレーションに対してクエリを実行したいことをクライアントに手動で知らせる必要があります。
getQuestion.ts と getQuestions.ts ファイルを以下のように変更します。

```
// app/questions/queries/getQuestion.ts
export default async function getQuestion({where /* include */}: GetQuestionInput, ctx: Ctx) {
  ctx.session.authorize()
  const question = await db.question.findFirst({where, include: {choices: true}})
  if (!question) throw new NotFoundError()
  return question
}
```

```
// app/questions/queries/getQuestions.ts
type GetQuestionsInput = Pick<FindManyQuestionArgs, "where" | "orderBy" | "cursor" | "take" | "skip">
export default async function getQuestions(
  {where, orderBy, cursor, take, skip}: GetQuestionsInput,
  ctx: Ctx,
) {
  ctx.session.authorize()
  const questions = await db.question.findMany({
    where,
    orderBy,
    cursor,
    take,
    skip,
    include: {choices: true},
  })
  const count = await db.question.count()
  const hasMore = typeof take === "number" ? skip + take < count : false
  const nextPage = hasMore ? { take, skip: skip + take! } : null
  return questions
}
```

次に、エディターのメインの質問ページに戻ります。
各質問の選択肢を一覧表示できます。 QuestionsListのリンクの下に次のコードを追加します。

```
<ul>
  {question.choices.map((choice) => (
    <li key={choice.id}>
      {choice.text} - {choice.votes} votes
    </li>
  ))}
</ul>
```

マジック！もう1つ、これらの質問に投票してもらいましょう。

エディターでapp / questions / pages / questions / [questionId] .tsxを開きます。
まず、このページを少し改善します。

1. `<h1> Question {question.id} </ h1>を<h1> {question.text} </ h1>に置き換えます。`
2. pre要素を削除し、前に作成した選択肢リストにコピーします。

ブラウザを見てください！こんなページになってるはずです。

次に、投票ボタンを追加します。私たちのliに、次のようなボタンを追加します。

```
<li key={choice.id}>
  {choice.text} - {choice.votes} votes
  <button>Vote</button>
</li>
```

次に、updateChoiceミューテーション（最初に生成されたもの）をインポートし、ページにhandleVote関数を作成します。

最後に、新しいボタンにその関数を呼び出すように指示します。

念のために変更したコードを全て載せておきます。

```
import React, {Suspense} from "react"
import {Head, Link, useRouter, useQuery, useParam, BlitzPage} from "blitz"
import getQuestion from "app/questions/queries/getQuestion"
import deleteQuestion from "app/questions/mutations/deleteQuestion"
import updateChoice from "app/choices/mutations/updateChoice" 
export const Question = () => {
  const router = useRouter()
  const questionId = useParam("questionId", "number")
  const [question, {refetch}] = useQuery(getQuestion, {where: {id: questionId}})
  const [deleteQuestionMutation] = useMutation(deleteQuestion)
  const [updateChoiceMutation] = useMutation(updateChoice) 
  const handleVote = async (id, votes) => {
    try {
      const updated = await updateChoiceMutation({
        where: {id},
        data: {votes: votes + 1},
      })
      refetch()
    } catch (error) {
      alert("Error creating question " + JSON.stringify(error, null, 2))
    }
  }
  return (
    <div>
      <h1>{question.text}</h1>
      <ul>
        {question.choices.map((choice) => (
          <li key={choice.id}>
            {choice.text} - {choice.votes} votes
            <button onClick={() => handleVote(choice.id, choice.votes)}>Vote</button>
          </li>
        ))}
      </ul>
      <Link href="/questions/[questionId]/edit" as={`/questions/${question.id}/edit`}>
        <a>Edit</a>
      </Link>
      <button
        type="button"
        onClick={async () => {
          if (window.confirm("This will be deleted")) {
            await deleteQuestionMutation({where: {id: question.id}})
            router.push("/questions")
          }
        }}
      >
        Delete
      </button>
    </div>
  )
}
const ShowQuestionPage: BlitzPage = () => {
  return (
    <div>
      <Head>
        <title>Question</title>
        <link rel="icon" href="/favicon.ico" />
      </Head>
      <main>
        <p>
          <Link href="/questions">
            <a>Questions</a>
          </Link>
        </p>
        <Suspense fallback={<div>Loading...</div>}>
          <Question />
        </Suspense>
      </main>
    </div>
  )
}
export default ShowQuestionPage
```

## 結論

おめでとうございます！あなたはあなた自身のBlitzアプリを作成しました！それで遊んだり、友達と共有したりして楽しんでください。
このチュートリアルが終了したので、投票アプリをさらに改善してみませんか？

良かったら試してみてね↓

- スタイルを当てる
- 投票の統計を表示する
- バーセルにデプロイする

プロジェクトを世界中のBlitzコミュニティと共有したい場合は、Slackよりも優れた場所はありません。
 slack.blitzjs.comにアクセスします。次に、＃show-and-tellチャンネルへのリンクを投稿して、みんなと共有しましょう！