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

## Migrating to Emotion 10

 [翻訳元](https://emotion.sh/docs/migrating-to-emotion-10)

Emotion10への移行

Emotion 10 は Emotion の重要な変更点ですので、コードの変更が必要になります。

いくつかの変更はコードモッドを使って自動的に行うことができますが、残りの変更は段階的に行うことができます。

このページは、Emotion with React を使用している場合にのみ適用されます。Emotion with React を使用していない場合は、何も変更する必要はありません。

Emotion 10 は、React 16.3 以上が必要です。

Emotion 10で最も大きな変更点は、基本となるクラス名に簡単にアクセスできなくなったことです。クラス名で考えるのではなく、スタイルを考えて合成する必要があります

（クラス名を直接使うことはできますが、ゼロコンフィグサーバーレンダリングのような新しい機能はありません）。

たとえば、Emotion 9では、cssから2つのクラスがあり、それらをcxと一緒に構成していましたが、Emotion 10では、2つのスタイルを作成し、次のようにcsspropで一緒に構成します。

### Incremental Migration

(増分の移行)

Emotion 10へのアップグレードは、2つの部分に分かれています。最初の部分は eslint-plugin-emotion を使うことで自動的に行うことができます。

#### Code moddable

それぞれの変更方法が記載されている

#### Manual Steps

プロバイダーとの互換キャッシュを追加する

この手順は、css、keyframes、またはemotionからinjectGlobalを引き続き使用する場合に必要です。アプリでそれらの使用法をすべて削除したら、これを削除できます。

#### Manual Steps Over Time

cssの使い方をcss propに変更する

wrapperClassNameなどのプロップスを受け付けるコンポーネントを持っている場合は、ClassNamesコンポーネントを利用することができます。

globalの書き方が変わったよ！

