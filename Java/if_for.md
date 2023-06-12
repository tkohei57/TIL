# Javaにおける条件分岐と繰り返し処理

## Javaにおける条件分岐
- if文の書き方
rubyにおける書き方と大きな違いはない。
```Java
if (条件式)　{
  処理
}
```

```Java
if (条件式1)　{
  処理1
} else if (条件式2) {
  処理2
} else {
  処理3
}
```

## Javaにおける繰り返し処理の基本事項
- 拡張for文
rubyにおけるeach文にあたる。
```Java
for ( 要素を格納する変数宣言  :  配列あるいはArrayListの変数名) {
  取り出した要素を使用して行う処理
}
```

例1
```Java
int[] numbers = {1, 5, 10};

for (int number : numbers) {
  System.out.println(number);
}
```

例2
```Java
ArrayList<Integer> numbers = new ArrayList<Integer>();

numbers.add(1);
numbers.add(5);
numbers.add(10);
numbers.add(15);

for(int number : numbers) {
  System.out.println(number);  
}
```

- while文
rubyにおけるwhile文とほぼ同じ
```Java
while( 条件式 ) {
  処理文; // 条件式がtrueの場合、実行される
}
```
例
```Java
int number = 0;
while( number < 5 ) {
  System.out.println(number);
  number++;
}

// 実行結果
0
1
2
3
4
```


- for文

1.書き方
```Java
for(式1; 式2; 式3) {
  処理文;
}
```
式1:カウント変数の宣言(初期化)

式2:条件式

式3:カウント変数の更新

例
```Java
for(int i = 0; i < 5; i++) {
  System.out.println(i);
}

// 実行結果
0
1
2
3
4
```

2.注意点
- 式1は文でなければならない（変数名のみなどはエラーになる）。
- 式1で複数に及ぶ式の宣言をしてはならない(,で区切ることで複数記述することは可能)。
- 式3でも,で区切ることで複数の処理を書くことができる。
