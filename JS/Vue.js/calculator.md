# Vue.jsを使用して電卓のミニアプリを作成してみる

## 数字を表示するエリア、数字・演算子のボタンを実装する

- Vueインスタンスのdataにcountを用意し、その内容を電卓画面に表示する
- v-forディレクティブを使用して数字や演算子のボタンを実装

```html
<div id="app">
  <div class="headline">
    {{title}}
  </div>
  <div class="input-form">
    <div class="box">
      {{count}}
    </div>
    <!-- <input type="text" :value="count" id="calc-form"> -->
    <div class="number-buttons">
      <button v-for="number in numbers" v-bind:key="number" class="number-button">
        {{number}}
      </button>
    </div>
    <div class="operate-buttons">
      <button v-for="operator in operators" v-bind:key="operator" class="operate-button">
        {{operator}}
      </button>
    </div>
    <div class="calc-button">
      <button>=</button>
    </div>
    <div class="reset-button">
      <button>C</button>
    </div>
  </div>
</div>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      title: "電卓！",
      numbers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9,],
      operators: ["+", "-", "*", "/"],
      count: "0",
    },
  });
</script>
```

## ボタンを押したときに呼び出されるメソッドを追加する。

- v-onディレクティブ（コード中では@で省略）でそれぞれのボタンが押された時に呼び出されるメソッドを定義し、Vueインスタンス内のmethodsでそれぞれのメソッドの処理を記述
- calcNum()メソッドはevalメソッドを使用していたが、あまり使用することが推奨されていないため、今回はMath.jsを導入した

```html
<div id="app">
  <div class="headline">
    {{title}}
  </div>
  <div class="input-form">
    <div class="box">
      {{count}}
    </div>
    <!-- <input type="text" :value="count" id="calc-form"> -->
    <div class="number-buttons">
      <button @click="pushNum(number)" v-for="number in numbers" v-bind:key="number" class="number-button">
        {{number}}
      </button>
    </div>
    <div class="operate-buttons">
      <button @click="pushOperator(operator)" v-for="operator in operators" v-bind:key="operator" class="operate-button">
        {{operator}}
      </button>
    </div>
    <div class="calc-button">
      <button @click="calcNum()">=</button>
    </div>
    <div class="reset-button">
      <button @click="resetNum()">C</button>
    </div>
  </div>
</div>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      title: "電卓！",
      numbers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9,],
      operators: ["+", "-", "*", "/"],
      count: "0",
    },
    methods: {
      pushNum (number) {
        if (this.count == 0) {
          this.count = "";
        }
        this.count += number;
      },

      pushOperator (operator) {
        this.count += operator;
      },

      calcNum () {
        // return this.count = eval(this.count);
        return this.count = math.evaluate(this.count);
      },

      resetNum () {
        this.count = 0;
      }
    },
  });
</script>
```
