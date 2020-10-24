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

- フォールバックスタイルのセットにはselectorName_fallbackを使用します。
  - 修飾子と同様に、名前を一貫性のあるものにしておくと、より適切なブラウザでこれらのスタイルを上書きするスタイルとの関係を明らかにするのに役立ちます。
 
fallbackが少し難しい。

使う時は↑のやり方という認識で。
 
 
 
 
 
 
 
 
 
 
 

## Ordering


## Nesting


## Inline


## Themes