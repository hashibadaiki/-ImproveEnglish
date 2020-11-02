[翻訳元](https://github.com/airbnb/javascript/tree/master/react#airbnb-reactjsx-style-guide)

# Airbnb Reactガイド

## Basic Rules

- 1つのファイルに1つのReactコンポーネントのみをインクルードします。
- ただし、1つのファイルに複数のステートレスまたはピュアコンポーネントを含めることができます。
- 常にJSX構文を使用する。
- JSXではないファイルからアプリを初期化する場合を除き、React.createElementは使用しないでください。
- react/forbid-prop-typesは、arrayOf、objectOf、またはshapeを使用して、配列とオブジェクトが何を含むかを明示的に指定した場合にのみ、配列とオブジェクトを許可します。

ここは正直なに書いてるか不明

## Class vs React.createClass vs stateless

- 内部状態や参照がある場合は、React.createClassよりもReact.Componentを拡張したクラスを優先します。

```js
// bad
const Listing = React.createClass({
  // ...
  render() {
    return <div>{this.state.hello}</div>;
  }
});

// good
class Listing extends React.Component {
  // ...
  render() {
    return <div>{this.state.hello}</div>;
  }
}
```

- そして、状態やrefを持たない場合は、クラスよりも通常の関数（矢印関数ではなく）を好みます。

```js
// bad
class Listing extends React.Component {
  render() {
    return <div>{this.props.hello}</div>;
  }
}

// bad (relying on function name inference is discouraged)
const Listing = ({ hello }) => (
  <div>{hello}</div>
);

// good
function Listing({ hello }) {
  return <div>{hello}</div>;
}
```

## Mixins

Mixinsは使わないでね＾＾（廃れた技術なので）

## Naming

- このESlintを使いましょう
`react/jsx-filename-extension`
- ファイル名はパスカルケースで
- ReactのコンポーネントにはPascalCaseを、そのインスタンスにはcamelCaseを使います。

- コンポーネント名としてファイル名を使用します。例えば、ReservationCard.jsxはReservationCardという参照名を持つ必要があります。ただし、ディレクトリのルートコンポーネントの場合は、index.jsxをファイル名として使用し、ディレクトリ名をコンポーネント名として使用します。

```js
// bad
import Footer from './Footer/Footer';

// bad
import Footer from './Footer/index';

// good
import Footer from './Footer';
```

- 高次のコンポーネントの名前と、渡されたコンポーネントの名前を合成したものを、生成されたコンポーネントのdisplayNameとして使用します。例えば、高次のコンポーネント withFoo() は、コンポーネント Bar を渡すと、withFoo(Bar) の displayName を持つコンポーネントを生成しなければなりません。
  - コンポーネントの displayName は、開発者ツールやエラーメッセージで使用される可能性があり、この関係を明確に表現する値を持つことで、何が起こっているのかを理解するのに役立ちます。

- DOM コンポーネントのプロップ名を目的別に使うのは避けましょう。
  - 人々は style や className のようなプロップが特定の意味を持つことを期待しています。アプリのサブセットに対してこの API を変化させると、コードの可読性やメンテナンス性が低下し、バグが発生する可能性があります。

```js
// bad
<MyComponent style="fancy" />

// bad
<MyComponent className="fancy" />

// good
<MyComponent variant="fancy" />
```

## Declaration

displayNameは使わないで！

## Alignment(配置)

`react/jsx-closing-bracket-location` `react/jsx-closing-tag-location`

このどちらかのlint使ってね

```js
// bad
<Foo superLongParam="bar"
     anotherSuperLongParam="baz" />

// good
<Foo
  superLongParam="bar"
  anotherSuperLongParam="baz"
/>
```

まぁようは見易く書いてって話

## Quotes

- JSX属性には必ずダブルクォート(")を使用し、その他のJSにはシングルクォート(')を使用します。
  - 通常のHTML属性も通常はシングルではなくダブルクォートを使用するので、JSX属性はこの慣習を反映しています。

## Spacing

## Props

## Refs

## Parentheses

## Tags

## Methods

## Ordering

## isMounted