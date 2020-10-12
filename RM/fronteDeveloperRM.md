# Frontend Developer RoadMap

[翻訳元](https://roadmap.sh/frontend)

- 紫チェック…おすすめ！
- 緑チェック…紫選ばないならこっち
- 灰チェック…今やらなくてもいい
- 灰…おすすめしない

恐らく 黄色 > 肌色 > 灰色

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

## 12.Modern CSS

## 13.Web Components
[Web Components](https://developer.mozilla.org/ja/docs/Web/Web_Components)




## 14.CSS Framework

## 15.Test App

## 16.Type Checker

## 17.Progressive Web App
Webサイトをスマホアプリのようにダウンロードできる技術

[PWA](https://developer.mozilla.org/ja/docs/Web/Progressive_web_apps)

## 18.SSR

## 19.GraphQL

## 20.SSG

## 21.Mobile App

## 22.Desktop App

## 23.Web Assembly

- JSは様々な対応ができるが、それだけでは3Dなどに対応できない
- その足りない部分を低水準言語(C++/Rust等)で補う
- Web Assembly自体は仕様が未確定の部分が多い


[Web Assembly](https://developer.mozilla.org/ja/docs/WebAssembly/Concepts)