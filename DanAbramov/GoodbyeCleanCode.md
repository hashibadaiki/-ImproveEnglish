[翻訳元](https://overreacted.io/goodbye-clean-code/)

# Goodbye, Clean Code

## それは夕暮れ時のことでした。

同僚が一週間ずっと書いていたコードをチェックしてきました。
私たちはグラフィックエディタのキャンバスで作業をしていたのですが、彼らは長方形や楕円のような図形の端に小さなハンドルをドラッグしてサイズを変更する機能を実装していました。

うまく動きました。

しかし、それはあまり良くなかった。同じような処理が書かれていたのです。
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

私には良い考えがありました。
代わりに下記のようにコードをグループ化することで、重複をすべて取り除くことができます。

```js
let Directions = {
  top(...) {
    // 5 unique lines of math
  },
  left(...) {
    // 5 unique lines of math
  },
  bottom(...) {
    // 5 unique lines of math
  },
  right(...) {
    // 5 unique lines of math
  },
};

let Shapes = {
  Oval(...) {
    // 5 unique lines of math
  },
  Rectangle(...) {
    // 5 unique lines of math
  },
}

let {top, bottom, left, right} = Directions;

function createHandle(directions) {
  // 20 lines of code
}

let fourCorners = [
  createHandle([top, left]),
  createHandle([top, right]),
  createHandle([bottom, left]),
  createHandle([bottom, right]),
];
let fourSides = [
  createHandle([top]),
  createHandle([left]),
  createHandle([right]),
  createHandle([bottom]),
];
let twoSides = [
  createHandle([left]),
  createHandle([right]),
];

function createBox(shape, handles) {
  // 20 lines of code
}

let Rectangle = createBox(Shapes.Rectangle, fourCorners);
let Oval = createBox(Shapes.Oval, fourSides);
let Header = createBox(Shapes.Rectangle, twoSides);
let TextBox = createBox(Shapes.Rectangle, fourCorners);
```

コードは全体の半分の大きさになり、重複が完全になくなりました! とてもすっきりした。
特定の方向や形の挙動を変えたいときに、あちこちのメソッドを更新するのではなく、一箇所でできるようになりました。

もう夜遅くになってしまいました（夢中になってしまいました）。
自分のコードをmasterにpushして、同僚のごちゃごちゃしたコードをどうやって巻き取ったかを自慢しながら就寝しました。

## 翌朝

...期待通りにはいきませんでした。

私の上司は一対一のチャットのために私を招待してくれました。
彼らは丁重に私の変更を元に戻すように頼みました。
信じられなかった。古いコードは汚く不便で、私のコードは保守性が高く見やすいコードなのに！

私はしぶしぶ承諾しましたが、彼らが正しかったことに気づくまで何年もかかりました。

## フェーズです

クリーンなコードに執着し、重複を排除することは、多くの人が経験することです。
自分のコードに自信が持てないとき、自分の価値やプロとしての誇りを測れるものに執着したくなります。
厳格なリントルール、命名スキーマ、ファイル構造、重複の欠如。

重複除去を自動化することはできませんが、練習すれば簡単にできるようになります。
重複が少ないか多いかは、変更のたびに大抵わかります。
その結果、重複を取り除くことは、コードに関する客観的な指標を改善することのように感じます。
さらに悪いことに、それは人々のアイデンティティの感覚を混乱させます。
私はクリーンなコードを書くタイプの人間だと。
これはある種の自己欺瞞と同じくらい強力です。

抽象化を作成する方法を学ぶと、その能力に興奮して、反復的なコードを見るたびに抽象化してしまいたくなります。
コーディングを始めて数年経つと、いたるところで繰り返しを目にするようになります。
もし誰かが抽象化は美徳だと言ったら、私たちはそれを食べてしまうでしょう。
そして、「清潔さ」を崇拝していない人を批判し始めるでしょう。

私の「リファクタリング」は、2つの意味で大失敗だったことがわかりました。

1. まず、書いた人とは話をしていません。コードを書き直して、その人の確認なしに修正しました。たとえそれが改善されていたとしても（もう信じられませんが）、これはひどいやり方です。健全なエンジニアリングチームは常に信頼関係を築いています。チームメイトのコードを議論なしに書き換えることは、一緒にコードベースを効果的に共同作業する能力に大きな打撃を与えます。
2. 私のコードは、重複を減らすために要件を変更する能力をトレードしましたが、それは良いトレードではありませんでした。例えば、私たちは後になって、異なる形状の異なるハンドルのために多くの特殊なケースや動作を必要としました。オリジナルの「厄介な」バージョンでは、そのような変更はケーキのように簡単でしたが、私の抽象化はその数倍複雑にならざるを得ませんでした。

