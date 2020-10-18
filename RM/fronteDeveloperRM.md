# Frontend Developer RoadMap

[翻訳元](https://roadmap.sh/frontend)

恐らくブロックの色の優先順位は 黄色 > 肌色 > 灰色

- <font color="Purple">紫色</font>…おすすめ！
- <font color="Green">緑色</font>…紫選ばないならこっち
- <font color="Blue">青色</font>…今やらなくてもいい
- <font color="Red">赤色</font>…おすすめしない

## 1.Internet

1-1.インターネットの仕組み

1-2.ブラウザとその仕組み

1-3.DNSとその仕組み

1-4.HTTPってなに？

1-5.ドメインってなに？

1-6.ホスティングってなに？

## 2.HTML

2-1.基礎を学ぶ

2-2.フォームとバリデーション

2-3.convensionsとベストプラックティス

[ベストプラックティス](https://github.com/hail2u/html-best-practices/blob/master/README.ja.md)

ようは良い慣例みたいな意味。

2-4.セマンティックなHTML

2-5.SEO

2-6.アクセシビリティ

## 3.CSS

3-1.基礎を学ぶ

3-2.レイアウト(flex/Gridなどなど)

3-3.レスポンシブ

## 4.JavaScript

4-1.基本的な構文

4-2.DOMの操作方法

4-3.API取得/Ajax

4-4.ES6/JSモジュール

[JS モジュール](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Modules)

4-5.ホスティング、イベントバンドラー、スコープ、プロトタイプ、Shadow DOM、strictのコンセプトを理解する

## 5.Version Control

5-1.Git

5-2.GitHub

## 6.Web Security Knowledge
Webのセキュリティに関する知識

6-1.HTTPS

[HTTPS](https://developer.mozilla.org/ja/docs/Glossary/https)

6-2.CORS

Webアプリから別のWebサーバーへのアクセスを、許可できる仕組み。

[CORS/MDN](https://developer.mozilla.org/ja/docs/Glossary/CORS)

[CORS/Qiita](https://qiita.com/att55/items/2154a8aad8bf1409db2b)

6-3.コンテンツセキュリティポリシー (CSP)

特定の攻撃を検知し、影響を軽減できるセキュリティレイヤー。

Webサーバーでの設定や、<meta>タグ内などで設定可能

[CSP](https://developer.mozilla.org/ja/docs/Web/HTTP/CSP)

6-4.OWASP security risks

OWASPという組織が毎年更新している、セキュリティの注意喚起。

[OWASP Japan](https://owasp.org/www-chapter-japan/)


## 7.Package Managers

どちらか1つを選んでも、両方学んでも大差はありません。

7-1.npm

7-2.yarn

## 8.CSS Architecture
命名規則

最新のフレームワークやCSS-in-JSを使用するとこれらを「覚えなきゃ！」と心配しなくてもいいけど、BEMぐらいは知っておいていいと思うよ。

8-1.BEM

8-2.OOCSS

8-3.SMACSS

## 9.CSS Preprocessors
[CSSプリプロセッサー](https://developer.mozilla.org/ja/docs/Glossary/CSS_preprocessor)

それほど必要ないものかもしれない。命名規則とにたレベル感で良い。

9-1.Sass

9-2.PostCSS

[PostCSSまとめ](https://qiita.com/morishitter/items/4a04eb144abf49f41d7d)

9-3.Less

[とほほのLess入門](http://www.tohoho-web.com/ex/less.html)

## 10.Build Tools

使ってはいるけど内部構造などを把握していない

### Task Runners

10-1.npm script

10-2.Gulp

### Module Bundlers

10-3.Webpack

10-4.Rollup

10-5.Parcel

### Linters and Formatters

10-6.Prettier

10-7.ESLint

10-8.StandardJS

## 11.Framework(Library)

### React

11-1.Redux

11-2.MobX

### Angular

11-3.RxJS

11-4.NgRx

### Vue

11-5.VueX

## 12.Modern CSS

12-1.Styled Components

12-2.CSS Modules

12-3.Styled JSX

12-4.Emotion

12-5.Radium

12-6.Glamorous

## 13.Web Components

[Web Components](https://developer.mozilla.org/ja/docs/Web/Web_Components)

13-1.HTML Templates

13-2.Custom Elements

13-3.Shadow DOM

## 14.CSS Framework

JSベースで、フレームワークベースのJavaScriptアプリケーションで使用するのが良いでしょう。

14-1.Reactstrap

14-2.Material UI

14-3.Tailwind CSS

14-4.Chakra UI

デフォルトでJavaScriptコンポーネントが付属していないCSSファーストのフレームワーク

14-5.Bootstrap

14-6.Materialize CSS

14-7.Bulma

## 15.Test App

ユニットテスト、インテグレーションテスト、機能テストの違いを学び、下記のツールを使ってテストの書き方を学びます。

15-1.Jest

15-2.react-testing-library

15-3.Cypress

15-4.Enzyme

これだけですべてのテストのニーズを満たすことができます。

15-5.その他

Mocha/Chai/Ava/Jamine

## 16.Type Checkers

16-1.TypeScript

16-2.Flow

## 17.Progressive Web App
Webサイトをスマホアプリのようにダウンロードできる技術

[PWA](https://developer.mozilla.org/ja/docs/Web/Progressive_web_apps)

PWAで使用されるさまざまなWeb APIを学ぶ

17-1.Storage

17-2.Wb Sockets

17-3.Service Workers

17-4.Location

17-5.Notificaitons

17-6.Device Orientation

17-7.Payments

17-8.Credentials

計算し、測定し、パフォーマンスを向上させる

17-9.PRPL Pattern

17-10.RAIL Model

17-11.Performance Metrics

17-12.Using Lighthouse

17-13.Using DevTools

## 18.SSR

### React

18-1.Next

18-2.After

### Angular

18-3.Universal

### Vue

18-4.Nuxt

## 19.GraphQL

RESTful Web API（REST）の持つ問題を解決するために開発された規格です。

19-1.Apollo

19-2.Relay Modern

## 20.SSG

## 21.Mobile App

## 22.Desktop App

## 23.Web Assembly

- JSは様々な対応ができるが、それだけでは3Dなどに対応できない
- その足りない部分を低水準言語(C++/Rust等)で補う
- Web Assembly自体は仕様が未確定の部分が多い


[Web Assembly](https://developer.mozilla.org/ja/docs/WebAssembly/Concepts)