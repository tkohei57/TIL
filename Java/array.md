# Javaにおける配列

## Rubyとの違い
- Javaの配列は、格納する要素の数を最初に決める必要がある。
- 後で要素数を変更することができない。
- 要素を増やす場合は、サイズの大きな配列を新たに作成して元データをコピーするか、ArrayListというリストの一種を使用する。

## 配列の定義
1.配列の宣言
```Java
int[] numbers;
```
→int型の配列numbersを宣言

2.配列の要素数を宣言
```Java
int[] numbers;
numbers = new int[3];
```
→int型で要素数が3の配列を変数numbersに代入

※1と2を以下のように同時に書くことも可能
```Java
int[] scores = new int[3];
```

※型推論で書くことも可能
```Java
　var scores = new int[3];
```

3.要素に値を代入する
```Java
int[] numbers;
numbers = new int[3];
numbers[0] = 1;
numbers[1] = 4;
numbers[2] = 14;
```

※1~3までを全て同時に書くことも可能
```Java
int[] scores = {1, 4, 14};
```
→代入する値が全て決まっている場合のみ

4.配列の要素を表示する
- 要素を一つ取り出して表示する
```Java
System.out.println(numbers[0]);
```

- 要素を全て取り出して表示する
```Java
System.out.println(Arrays.toString(numbers));
```
※ファイルの先頭に"import java.util.Arrays;"を記述し、ライブラリをインポートする必要あり？

## ArrayList
長さ（要素数）を変更できる配列(可変長配列)のこと

## ArrayListの使い方
1.ライブラリのインポート
ファイルの先頭に以下のコードを記述する
```Java
import java.util.ArrayList;
```

2.ArrayListの宣言を行う
```Java
ArrayList<データ型> numbers = new ArrayList<データ型>();
```

```Java
ArrayList<Integer> numbers = new ArrayList<Integer>();
```
→変数numbersにInteger型のArrayListを宣言

※右辺のデータ型は省略可能
```Java
ArrayList<Integer> numbers = new ArrayList<>();
```

3.値を代入する
```Java
numbers.add(1);　　// 配列に1を追加
```
→addメソッドを使用して値を追加(値は配列の末尾に追加される)

4.要素を取り出す
- 要素を一つ取り出して表示する
※要素の取得
```Java
numbers.get(0);　　// 配列の1番目の要素を取得
```

```Java
System.out.println(numbers.get(0));
```

- 要素を全て取り出して表示する
```Java
System.out.println(numbers.toString());
```
