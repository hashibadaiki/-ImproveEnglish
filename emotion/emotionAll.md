# emotion全体

ざっとみた内容をまとめていく

全て感想。あとから書き足す。

## Server Side Rendering

[翻訳元](https://emotion.sh/docs/ssr)

このページはSSRについて。

2つの方法があるが基本はデフォルトで良い。

advanceなやり方はcacheを使うっぽい

## Attaching Props

[翻訳元](https://emotion.sh/docs/with-props)

propの当て方について書いている

```js
const pinkInput = css`
  background-color: pink;
`;
```
おそらくこの書き方のことを言っている

## Theming

[翻訳元](https://emotion.sh/docs/theming)

テーマ

テーマはemotionのテーマによって提供されます

ThemeProviderをアプリのトップレベルに追加し、スタイル付きコンポーネントのprops.themeを使用してテーマにアクセスするか、テーマをcsspropとして受け入れる関数を提供します。 

APIは、ドキュメントに詳細に記載されています。

つまり、これはざっくり書くとテーマっていうパッケージの説明。

cssPROP/styled/hookの3種類で使えるって話


## Labels

[翻訳元](https://emotion.sh/docs/labels)

babel-plugin-emotion は変数名やその他の情報に基づいて自動的にラベルを追加するので、手動で指定する必要はありません。

ハッシュ値を使ってラベリングしている模様

## CacheProvider

 [翻訳元](https://emotion.sh/docs/cache-provider)

例えば、カスタムStylisプラグインの追加、挿入されるクラス名の接頭辞のカスタマイズ、特定の要素にスタイルタグをレンダリングするなど、エモーションのオプションをカスタマイズするのに便利です。

`import createCache from '@emotion/cache'
`

これを宣言して様々なoptionをつけられるという認識