[翻訳元](https://emotion.sh/docs/object-styles)

# ObjectStyles

オブジェクトでスタイルを書くというのは、emotion@core に直接組み込まれた強力なパターンです。

通常の css のようにケバブケースでプロパティを書くのではなく、キャメルケースで書き、例えば background-color は backgroundColor になります。

オブジェクトスタイルは、文字列スタイルのように css を呼び出す必要がないので、css プロップと一緒に使うと特に便利ですが、オブジェクトスタイルは styled と一緒に使うこともできます。

## 結論(このページから自分の感じたこと)

つまり css を変数のようにするのではなく、直接オブジェクトに記述すること？

記述の方法

## 例えば

### With the css prop

css prop を使った書き方

```js
/** @jsx jsx */
import { jsx } from "@emotion/core";

render(
  <div
    css={{
      color: "darkorchid",
      backgroundColor: "lightgray",
    }}
  >
    This is darkorchid.
  </div>
);
```

### With styled

styled を使った書き方

```js
import styled from "@emotion/styled";

const Button = styled.button(
  {
    color: "darkorchid",
  },
  (props) => ({
    fontSize: props.fontSize,
  })
);

render(<Button fontSize={16}>This is a darkorchid button.</Button>);
```

### Child Selectors

ネストしている時の書き方

```js
/* @jsx jsx */
import { jsx } from "@emotion/core";

render(
  <div
    css={{
      color: "darkorchid",
      "& .name": {
        color: "orange",
      },
    }}
  >
    This is darkorchid.
    <div className="name">This is orange</div>
  </div>
);
```

### Media Queries

```js
/** @jsx jsx */
import { jsx } from "@emotion/core";

render(
  <div
    css={{
      color: "darkorchid",
      "@media(min-width: 420px)": {
        color: "orange",
      },
    }}
  >
    This is orange on a big screen and darkorchid on a small screen.
  </div>
);
```

### Numbers

特に指定しない場合は px が付与される

```js
/** @jsx jsx */
import { jsx } from "@emotion/core";

render(
  <div
    css={{
      padding: 8,
      zIndex: 200,
    }}
  >
    This has 8px of padding and a z-index of 200.
  </div>
);
```

### Arrays

配列にして指定することは理解できたけど、使いどころは不明

```js
/** @jsx jsx */
import { jsx } from "@emotion/core";

render(
  <div
    css={[
      { color: "darkorchid" },
      { backgroundColor: "hotpink" },
      { padding: 8 },
    ]}
  >
    This is darkorchid with a hotpink background and 8px of padding.
  </div>
);
```

### Fallbacks

配列の機能をサポートしていないブラウザのフォールバック値を定義します。
これも使いどころは不明

```js
/** @jsx jsx */
import { jsx } from "@emotion/core";

render(
  <div
    css={{
      background: ["red", "linear-gradient(#e66465, #9198e5)"],
      height: 100,
    }}
  >
    This has a gradient background in browsers that support gradients and is red
    in browsers that don't support gradients
  </div>
);
```

### With css

css を使うことも可能です

```js
/** @jsx jsx */
import { jsx, css } from "@emotion/core";

const hotpink = css({
  color: "hotpink",
});

render(
  <div>
    <p css={hotpink}>This is hotpink</p>
  </div>
);
```

### Composition

Composition で書くとこんな感じ

```js
/** @jsx jsx */
import { jsx, css } from "@emotion/core";

const hotpink = css({
  color: "hotpink",
});

const hotpinkHoverOrFocus = css({
  "&:hover,&:focus": hotpink,
});

const hotpinkWithBlackBackground = css(
  {
    backgroundColor: "black",
    color: "green",
  },
  hotpink
);

render(
  <div>
    <p css={hotpink}>This is hotpink</p>
    <button css={hotpinkHoverOrFocus}>This is hotpink on hover or focus</button>
    <p css={hotpinkWithBlackBackground}>
      This has a black background and is hotpink. Try moving where hotpink is in
      the css call and see if the color changes.
    </p>
  </div>
);
```
