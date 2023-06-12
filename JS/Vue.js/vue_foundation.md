# Vue.jsについて

## Vue.jsとは
アプリケーション開発において、UIを構築するためのJavaScriptフレームワークのこと。扱うデータやイベントが多くなっても、コードが複雑になりにくいという特長がある。

## 基本的な書き方
```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="utf-8">
    <title>Vue.js</title>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script> <!-- CDNでVue.jsを読み込む -->
  </head>
  <body>
    <div id="app">
      {{ greet }} <!-- VueインスタンスのデータをHTMLのテキストとして表示 -->
    </div>
    <script src="main.js">
    </script>
  </body>
</html>
```
```js
const app = new Vue({             // Vueインスタンスを生成し変数に代入
  el: '#app',                 // elオプションで適用する範囲を指定
  data: {                         // dataオプション内で使用するデータを設定
    greet: 'こんにちは!',
  },
});
```

## データバインディング
Vue.jsで使う特別な属性であるディレクティブを使用する

- v-bind
→要素の属性値にVueインスタンスのデータを結びつけることができる

例
```html
<div id="app">
  <a v-bind:href="url">aaa</a>
</div>
```
```js
const app = new Vue({
  el: '#app',
  data: {
    url: 'https://aaa.jp/',  // htmlのaタグのhref属性の値を記述
  },
});
```

- v-for
→配列またはオブジェクトを繰り返し処理して表示

例
```html
<ul id="app">
  <li
   v-for="member in members" <!-- 配列membersの要素の数だけ繰り返し処理を行い、それぞれの要素が一つずつ変数memberに代入される -->
   v-bind:key="member" <!-- v-bindでkey属性にmemberと書くことでそれぞれの値がmemberキーに対するバリューとなる -->
  >
    {{ member }}
  </li>
</ul>
```
```js
const app = new Vue({
  el: '#app',
  data: {
    members: ['a', 'b', 'c', 'd'], // 配列を定義
  },
});
```

- v-on
→イベントの処理

```html
<div id="app">
  <input
    v-bind:value="name"
    v-on:input="name = $event.target.value"  <!-- inputイベントが発生したらそれに続く処理を実行する -->
  >
  <p>{{ name }}</p>
</div>
```
```js
const app = new Vue({
  el: '#app',
  data: {
    name: '太郎',
  },
});
```
※イベントが起きると、発生したイベントの情報などが格納された「イベントオブジェクト」が生成される。
Vueの場合、$eventという特別な変数が、イベントオブジェクトにアクセスするための変数となる。

- ディレクティブの省略記法

1.v-bind:は:のみで表記できる。
2.v-on:は@のみで表記できる。
例
```html
<input @input="name = $event.target.value" :value="name">
```

- v-model
→input要素の入力からデータを更新できるようにするため、先ほどはv-onディレクティブとv-bindディレクティブを使った。
しかしフォームに関するものはv-modelを使えばコードがよりシンプルになる。

例
```html
<div id="app">
  <input v-model="name"> <!-- v-modelを使用することでv-onとv-bindをまとめることができる -->
  <p>{{ name }}</p>
</div>
```
```js
const app = new Vue({
  el: '#app',
  data: {
    name: '太郎',
  },
});
```
```
<input v-model="Vueインスタンスのdataオプションに設定したプロパティ名"> <!-- 左のように書くだけで、「そのinput要素に関するイベントが発生したら、指定したデータの値を更新する」という処理が行われる。 -->
```

## 算出プロパティ
複雑な処理を行った結果をhtml上に表示したい場合は算出プロパティを使用する。
- 書き方
```html
<div id="app">
  <div>
    {{ computed_name }} <!-- 算出プロパティの呼び出し -->
  </div>
</div>
```
```js
const app = new Vue({
  el: '#app',
  data: {
  
  },
  computed: {
    computed_name() {
      // 処理を記述
    },
  },
});
```

## メソッド
先ほどの算出プロパティと同じように複雑な処理を行った結果をhtml上に表示したい場合は算出プロパティを使用する。

※メソッドをマスタッシュ構文で使う場合、呼び出すためには()が必要になる。

- 書き方
```html
<div id="app">
  <div>
    {{ method_name() }} <!-- メソッドの呼び出し -->
  </div>
</div>
```
```js
const app = new Vue({
  el: '#app',
  data: {
  
  },
  methods: {
    method_name() {
      // 処理を記述
    },
  },
});
```

## 算出プロパティとメソッドの違い
- 算出プロパティ：参照しているVueインスタンスのデータが更新されたときだけ再計算される
- メソッド：イベントが起きる度に呼び出される。
