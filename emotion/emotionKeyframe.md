[翻訳元](https://emotion.sh/docs/keyframes)

# emotionのkeyfameについて

@ emotion / coreのkeyframesヘルパーを使用してアニメーションを定義できます。

keyframesは、cssキーフレーム定義を受け取り、スタイルで使用できるオブジェクトを返します。 cssと同じように文字列またはオブジェクトを使用できます。

つまり、cssに埋め込むオブジェクトを作成できる。

```js
/** @jsx jsx */
import { jsx, css, keyframes } from '@emotion/core'

const bounce = keyframes`
  from, 20%, 53%, 80%, to {
    transform: translate3d(0,0,0);
  }

  40%, 43% {
    transform: translate3d(0, -30px, 0);
  }

  70% {
    transform: translate3d(0, -15px, 0);
  }

  90% {
    transform: translate3d(0,-4px,0);
  }
`

render(
  <div
    css={css`
      animation: ${bounce} 1s ease infinite;
    `}
  >
    some bouncing text!
  </div>
)
```