[翻訳元](https://overreacted.io/goodbye-clean-code/)

# Goodbye, Clean Code

それは遅い夕暮れ時でした。

同僚が一週間ずっと書いていたコードをチェックしてきました。
私たちはグラフィックエディタのキャンバスで作業をしていたのですが、彼らは長方形や楕円のような図形の端に小さなハンドルをドラッグしてサイズを変更する機能を実装していました。

うまく動きました。

しかし、それはあまり良くなかった。同じような処理が書かれていた。
各図形（矩形や楕円など）にはそれぞれ異なるハンドルのセットがあり、それぞれのハンドルを異なる方向にドラッグすると、図形の位置やサイズに異なる影響を与えていました。
ユーザーが Shift キーを押したままであれば、サイズを変更する際にプロポーションを維持する必要があります。これには多くの計算が必要でした。

コードは次のような感じでした。

```js
let Rectangle = {
  resizeTopLeft(position, size, preserveAspect, dx, dy) {
    // 10 repetitive lines of math
  },
  resizeTopRight(position, size, preserveAspect, dx, dy) {
    // 10 repetitive lines of math
  },
  resizeBottomLeft(position, size, preserveAspect, dx, dy) {
    // 10 repetitive lines of math
  },
  resizeBottomRight(position, size, preserveAspect, dx, dy) {
    // 10 repetitive lines of math
  },
};

let Oval = {
  resizeLeft(position, size, preserveAspect, dx, dy) {
    // 10 repetitive lines of math
  },
  resizeRight(position, size, preserveAspect, dx, dy) {
    // 10 repetitive lines of math
  },
  resizeTop(position, size, preserveAspect, dx, dy) {
    // 10 repetitive lines of math
  },
  resizeBottom(position, size, preserveAspect, dx, dy) {
    // 10 repetitive lines of math
  },
};

let Header = {
  resizeLeft(position, size, preserveAspect, dx, dy) {
    // 10 repetitive lines of math
  },
  resizeRight(position, size, preserveAspect, dx, dy) {
    // 10 repetitive lines of math
  },  
}

let TextBlock = {
  resizeTopLeft(position, size, preserveAspect, dx, dy) {
    // 10 repetitive lines of math
  },
  resizeTopRight(position, size, preserveAspect, dx, dy) {
    // 10 repetitive lines of math
  },
  resizeBottomLeft(position, size, preserveAspect, dx, dy) {
    // 10 repetitive lines of math
  },
  resizeBottomRight(position, size, preserveAspect, dx, dy) {
    // 10 repetitive lines of math
  },
};
```

繰り返しの算数がすごく気になっていました。

すっきりしていなかった。

繰り返しのほとんどは、似たような方向の間で行われていました。
例えば、Oval.resizeLeft() は Header.resizeLeft() と類似していました。
これは、どちらも左側のハンドルをドラッグすることを扱っていたからです。

もう一つの類似点は、同じ形状のメソッド間にありました。
例えば、Oval.resizeLeft() は他の Oval メソッドと類似していました。
これは、それらがすべて楕円を扱っていたからです。
また、テキストブロックが矩形であったため、Rectangle、Header、TextBlockの間にも重複がありました。

私には考えがありました。

代わりにこのようにコードをグループ化することで、重複をすべて取り除くことができます。