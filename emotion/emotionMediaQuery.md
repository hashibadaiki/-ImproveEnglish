[翻訳元](https://emotion.sh/docs/media-queries
)

# emotion mediaQuery

emotion のメディアクエリアは通常の CSS と似た書き方をします。
例えば ↓ みたいな感じ

```js
/** @jsx jsx */
import { jsx, css } from "@emotion/core";

render(
  <p
    css={css`
      font-size: 30px;
      @media (min-width: 420px) {
        font-size: 50px;
      }
    `}
  >
    Some text!
  </p>
);
```

## 再利用可能なメディアクエリ

メディアクエリは再利用しないと面倒だし、不都合が多い。
↓ こんな感じで変数に入れたら使いまわせるよ！

```js
/** @jsx jsx */
import { jsx, css } from "@emotion/core";

const breakpoints = [576, 768, 992, 1200];

const mq = breakpoints.map((bp) => `@media (min-width: ${bp}px)`);

render(
  <div>
    <div
      css={{
        color: "green",
        [mq[0]]: {
          color: "gray",
        },
        [mq[1]]: {
          color: "hotpink",
        },
      }}
    >
      Some text!
    </div>
    <p
      css={css`
        color: green;
        ${mq[0]} {
          color: gray;
        }
        ${mq[1]} {
          color: hotpink;
        }
      `}
    >
      Some other text!
    </p>
  </div>
);
```

## facePaint

↑ の書き方だいぶ長いからもっと短くできるよ！
注意： facepaint はオブジェクトスタイルでのみ機能します。

```js
/** @jsx jsx */
import { jsx } from "@emotion/core";
import facepaint from "facepaint";

const breakpoints = [576, 768, 992, 1200];

const mq = facepaint(breakpoints.map((bp) => `@media (min-width: ${bp}px)`));

render(
  <div
    css={mq({
      color: ["green", "gray", "hotpink"],
    })}
  >
    Some text.
  </div>
);
```
