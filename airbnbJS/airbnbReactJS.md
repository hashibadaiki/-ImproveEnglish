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

## Declaration

## Alignment

## Quotes

## Spacing

## Props

## Refs

## Parentheses

## Tags

## Methods

## Ordering

## isMounted