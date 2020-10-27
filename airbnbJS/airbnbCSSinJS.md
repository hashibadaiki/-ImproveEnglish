[翻訳元](https://github.com/airbnb/javascript/tree/master/css-in-javascript)

# Airbnb CSS-in-JSガイド

## Naming

- オブジェクトのキーはキャメルケースを使いましょう
  - これらのキーはコンポーネント内のスタイルオブジェクトのプロパティとしてアクセスするので、キャメルケースを使うのが最も便利です。

 ```js
 // bad
{
  'bermuda-triangle': {
    display: 'none',
  },
}
// good
{
  bermudaTriangle: {
    display: 'none',
  },
}
 ```
 
- 他のスタイルへの修飾子(状態)にはアンダースコアを使用します。
   - どこを修正したいか？の意図が明確に伝わるので

 ```js
 // bad
{
  bruceBanner: {
    color: 'pink',
    transition: 'color 10s',
  },
  bruceBannerTheHulk: {
    color: 'green',
  },
}
// good
{
  bruceBanner: {
    color: 'pink',
    transition: 'color 10s',
  },
  bruceBanner_theHulk: {
    color: 'green',
  },
}
 ```

- フォールバックスタイルのセットにはselectorName_fallbackを使用します。
  - 修飾子と同様に、名前を一貫性のあるものにしておくと、より適切なブラウザでこれらのスタイルを上書きするスタイルとの関係を明らかにするのに役立ちます。
 
fallbackが少し難しい。

使う時は↑のやり方という認識で。
 
- フォールバックスタイルのセットには、別のセレクタを使用します。

  - フォールバックスタイルを別のオブジェクトに含めることで、その目的が明確になり、可読性が向上します。 
 
 ```js
// bad
{
  muscles: {
    display: 'flex',
  },
  left: {
    flexGrow: 1,
    display: 'inline-block',
  },
  right: {
    display: 'inline-block',
  },
}
// good
{
  muscles: {
    display: 'flex',
  },
  left: {
    flexGrow: 1,
  },
  left_fallback: {
    display: 'inline-block',
  },
  right_fallback: {
    display: 'inline-block',
  },
}
 ```

- メディアクエリのブレークポイントの名前には、デバイスに依存しない名前（例："small"、"medium"、"large"）を使用してください。

  - 「phone」、「tablet」、「desktop」のような一般的に使用されている名前は、現実世界のデバイスの特性と一致しません。これらの名前を使用すると、間違った期待を抱かせてしまいます。
 
 ```js
 // bad
const breakpoints = {
  mobile: '@media (max-width: 639px)',
  tablet: '@media (max-width: 1047px)',
  desktop: '@media (min-width: 1048px)',
};
// good
const breakpoints = {
  small: '@media (max-width: 639px)',
  medium: '@media (max-width: 1047px)',
  large: '@media (min-width: 1048px)',
};
 ```
 
## Ordering(順序)

- コンポーネントの後にスタイルを定義します。 
  - 高次のコンポーネントを使用してスタイルにテーマを設定します。これは、コンポーネントの定義後に自然に使用されます。スタイルオブジェクトをこの関数に直接渡すと、間接参照が減ります。

  ```js
  // bad
const styles = {
  container: {
    display: 'inline-block',
  },
};
function MyComponent({ styles }) {
  return (
    <div {...css(styles.container)}>
      Never doubt that a small group of thoughtful, committed citizens can
      change the world. Indeed, it’s the only thing that ever has.
    </div>
  );
}
export default withStyles(() => styles)(MyComponent);
// good
function MyComponent({ styles }) {
  return (
    <div {...css(styles.container)}>
      Never doubt that a small group of thoughtful, committed citizens can
      change the world. Indeed, it’s the only thing that ever has.
    </div>
  );
}
export default withStyles(() => ({
  container: {
    display: 'inline-block',
  },
}))(MyComponent);
  ```


## Nesting

- 同じインデントレベルで隣接するブロック間に空白の線を残します。

  - 空白にすることで可読性が向上し、マージ時の競合の可能性が減ります。

```js
// bad
{
  bigBang: {
    display: 'inline-block',
    '::before': {
      content: "''",
    },
  },
  universe: {
    border: 'none',
  },
}

// good
{
  bigBang: {
    display: 'inline-block',

    '::before': {
      content: "''",
    },
  },

  universe: {
    border: 'none',
  },
}
```

## Inline

- カーディナリティの高いスタイル (例: プロップの値を使用する) にはインラインスタイルを使用し、カーディナリティの低いスタイルには使用しないようにしてください。

  - テーマのあるスタイルシートを生成するのはコストがかかるので、個別のスタイルセットに最適です。

```js
// bad
export default function MyComponent({ spacing }) {
  return (
    <div style={{ display: 'table', margin: spacing }} />
  );
}

// good
function MyComponent({ styles, spacing }) {
  return (
    <div {...css(styles.periodic, { margin: spacing })} />
  );
}
export default withStyles(() => ({
  periodic: {
    display: 'table',
  },
}))(MyComponent);
```

## Themes

- react-with-styles のような、テーマ設定を可能にする抽象化レイヤーを使用します。 react-with-styles は withStyles()、ThemedStyleSheet、css() のようなものを提供してくれます。
  - コンポーネントのスタイリングのために共有変数のセットを持っていると便利です。抽象化レイヤーを使用することで、より便利になります。さらに、これはコンポーネントが特定の基礎となる実装に固く結合されるのを防ぐのに役立ち、より自由度が高まります。

  フォントやカラーは変数から使用しましょうねって話。
  
  ```js
  // bad
export default withStyles(() => ({
  chuckNorris: {
    color: '#bada55',
  },
}))(MyComponent);
// good
export default withStyles(({ color }) => ({
  chuckNorris: {
    color: color.badass,
  },
}))(MyComponent);
  ```