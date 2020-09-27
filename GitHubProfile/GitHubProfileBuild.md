# GituHubProfile

https://towardsdatascience.com/build-a-stunning-readme-for-your-github-profile-9b80434fe5d7

## 良い感じのGitHubprofileの作り方

他の人のGitHubに良い感じのprofile見たことない？あれはGitHubの新機能やで！
あの新しい機能のいい感じの使い方をこれから説明していくで！

## GitHubprofileの作り方
前回の翻訳とかぶってるので省略。
公式を載せ替えてるだけ

## 目立たせる方法
これで僕らはREADEMEが入ったリポジトリーを作ったわけだけど、何かコンテンツある？
emailアドレスとか入れて〜ってできるけど、もっといい方法があるんやで！

個性的なヘッダーをつけるといい感じにみえるよ！
あなたの名前か、職種を打ち込んでコンテンツをあげればいいよ！
沢山の良い例があるけど、以下の3つをピックアップするね！

どうやってREADMEに画像を追加するのですか？
まず最初に、写真をパブリックリポジトリーに入れて、その後READMEで呼び込みます

次の行をREADMEの先頭に入れてね！

`
[![Header](https://raw.githubusercontent.com/MartinHeinz/<OWNER>/<OWNER>/readme_header.png "Header")](https://some-url.dev/)
`

これは、基本的な画像を埋め込むマークダウンの書き方です。
Websiteに呼び込めるようにURLも含まれています

## GIFs 絵文字の使い方

gifとか絵文字を使ってもっとREADMEを楽しいものにできますよ！
私はタイトルの最初に絵文字をつけるのが好きです！例えば下の図みたいな感じ。

絵文字に関する簡単な方法見つけたよ！

`
https://emojipedia.org/emoji/
`

このURLから探したらOK。
実体は[こっち](https://www.fileformat.info/index.htm)にあるよ〜

もしこれで絵文字が足りなかったらGIFを追加できるよ。GIFを追加するときは、ヘッダー画像などのリポジトリ内またはhttps://imgur.com/などの外部Webサイトでホストされている実際の.gifファイルが必要です。

ホスティングされてない場合に使うときはこちら↓

`
<img src="https://raw.githubusercontent.com/<OWNER>/<OWNER>/master/<GIF_NAME>.gif" width="30px">
`

GitHubマークダウンで使えるHTMLタグは何個かあって、その中の一つが<img>やで。

<img>使えば簡単にimagesやGIFをREADMEに追加できます。

## あなたのリポジトリを紹介する

皆のGitHubプロフィールは、実績とかやってることを強調してるだけやで。
GitHubプロフィールを使って実績を強調したかったら、github-readme-statsを使うのがいいで。

これは、GitHubのステータスからやったこととか、リポジトリの中身をみて作られます。
もしあなたが全部許可してくれたら、下の図みたいなのができるよ〜

このカードたちはいくつかパターンがあって、それぞれカスタムできます。テーマ、言語、アイコンなどが選べます。
カードを作るときは以下のパターンがあるよ〜

`
<img align="center" src="https://github-readme-stats.vercel.app/api/<CARD_TYPE>/?username=<USERNAME>&theme=<THEME_NAME>" />
`

カードタイプは上位の言語リストか、ピンから選んでね。空白のままにしたらデフォルトの表記になります。
もっとカスタマイズしたったら、github-readme-stats repositoryか私のリポジトリを見てみてね〜

## あなたのスキルを強調しましょう

あとよく見かけるのは技術と技能のリストです。こんな感じ(下の図)。
こんなふうにいい感じにするには shields.ioを使います。

色んなスタイルがあるけど、私の好きなのは下の感じ！
これを作るときのマークダウンは下のやつを参考にして！

`
![](https://img.shields.io/badge/<WORD_ON_LEFT>-<WORD_ON_RIGHT>-informational?style=flat&logo=<LOGO_NAME>&logoColor=white&color=2bbc8a)
`

もしこの色好きじゃなかったら、[こっち](https://shields.io/)のサイト見て。

私のようにアイコンのファンならsimpleicons.org が便利かも知れない。ここで使われているアイコンがリスト化されているから。

もし、この中に使えないバッジがあったら、base64をダウンロードしてね。そのときは下みたいなマークダウンを書いてね。

`
![](https://img.shields.io/badge/<WORD_ON_LEFT>-<WORD_ON_RIGHT>-informational?style=flat&logo=data:image/svg%2bxml;base64,<BASE64_DATA>)
`

## ソーシャルメディアの読み込み

絶対にあなたへの連絡先をプロフィールに書いた（読み込んだ）方がいいよ！
emailでもTwitterでも他のソーシャルメディアでもいいよ。

どれを選択してもいいけど、アイコン＋リンクを使用して載せるべきやで。

下の感じのマークダウンを書いてね！

```
<!-- Actual text -->

You can find me on [![Twitter][1.2]][1], or on [![LinkedIn][3.2]][3].

<!-- Icons -->

[1.2]: http://i.imgur.com/wWzX9uB.png (twitter icon without padding)
[2.2]: https://raw.githubusercontent.com/MartinHeinz/MartinHeinz/master/linkedin-3-16.png (LinkedIn icon without padding)

<!-- Links to your social media accounts -->

[1]: https://twitter.com/Martin_Heinz_
[2]: https://www.linkedin.com/in/heinz-martin/
```

レンダリングされたマークダウンは下の図みたいに見えるよ。

## 結論

簡潔に書いたり、独創的であることも大事やけど、自分のものにすることが一番大切です。

うまくいけば、この記事はGitHubProfile作る時にインスピレーションを与えます。
この記事とは別に、私のGitHubも役立つかも。とかったら見てね。

もし、もっと他の例が見たかったらawesome-github-profile-readme.を見てね〜