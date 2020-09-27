[翻訳元](https://emotion.sh/docs/composition)

# Composition

compositionはめっちゃ便利なものです！
cssから返された値を別のスタイルに補間することで、
スタイルを一緒に構成できます。

```js
/** @jsx jsx */
import { jsx, css } from '@emotion/core'

const base = css`
  color: hotpink;
`

render(
  <div
    css={css`
      ${base};
      background-color: #eee;
    `}
  >
    This is hotpink.
  </div>
)
```

通常のCSSはimpost!合戦になるようになっている（破綻しやすい）

例えば↓の書き方やとどっちが優先されるか分かりにくくない？

```js
render(
  <div>
    <style>
      {`
        .danger {
          color: red;
        }
        .base {
          background-color: lightgray;
          color: turquoise;
        }
      `}
      >
    </style>
    <p className="base danger">What color will this be?</p>
  </div>
)
```

こんな状態もemotion使えば解決できるよ！
↓こんな感じ！

```js
/** @jsx jsx */
import { css, jsx } from '@emotion/core'

const danger = css`
  color: red;
`

const base = css`
  background-color: darkgreen;
  color: turquoise;
`

render(
  <div>
    <div css={base}>This will be turquoise</div>
    <div css={[danger, base]}>
      This will be also be turquoise since the base styles
      overwrite the danger styles.
    </div>
    <div css={[base, danger]}>This will be red</div>
  </div>
)
```
（配列で優先順位を示しているっぽい。試してみる）

compositionを使用すると使用順序で優先順位が決まって、書いた順序は関係ないよ！