[翻訳元](https://github.com/airbnb/javascript/tree/master/css-in-javascript)

# Airbnb CSS-in-JSガイド

## Naming

- オブジェクトのキーはキャメルケースを使いましょう
  - これらのキーはコンポーネント内のスタイルオブジェクトのプロパティとしてアクセスするので、キャメルケースを使うのが最も便利です。

 ```js
 // bad
{
  'bermuda-triangle': {
    display: 'none',
  },
}
// good
{
  bermudaTriangle: {
    display: 'none',
  },
}
 ```
 
- 他のスタイルへの修飾子(状態)にはアンダースコアを使用します。
   - どこを修正したいか？の意図が明確に伝わるので

 ```js
 // bad
{
  bruceBanner: {
    color: 'pink',
    transition: 'color 10s',
  },
  bruceBannerTheHulk: {
    color: 'green',
  },
}
// good
{
  bruceBanner: {
    color: 'pink',
    transition: 'color 10s',
  },
  bruceBanner_theHulk: {
    color: 'green',
  },
}
 ```

- Use selectorName_fallback for sets of fallback styles.こっから
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 

## Ordering


## Nesting


## Inline


## Themes