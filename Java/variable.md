# Javaでの変数について

## データ型
変数に格納しておくデータの種類のこと。基本として8種類存在する。

- 基本のデータ型

| データ型 | bit数 | 値 |
| :-- | :-: | --: |
| boolean | 1bit | true あるいは　false |
| char | 16bit | 文字 |
| byte | 8bit | 整数（扱える範囲は -128～127） |
| short | 16bit | 整数（扱える範囲は-32,768～32,767） |
| int | 32bit | 整数（扱える範囲は-2,147,483,648～2,147,483,647） |
| long | 64bit | 整数（扱える範囲は-9223372036854775808～9223372036854775807） |
| float | 32bit | 小数（精度低） |
| double | 64bit | 小数（精度高） |

- Javaにおいて、変数を定義する際はまずそのデータ型を宣言する必要がある。

## コードを記述する上での注意点
- 以下のコードは消さないようにする。
```Java
class Main {
  public static void main(String[] args) {
    //これより下に処理を記述していく
  }
}
```

## 変数を定義して半径が5cmの円の面積を求める
- 変数の定義方法
```Java
型名　変数名;
```

```Java
class Main {
  public static void main(String[] args) {
    int　radius;
    radius = 5;
    System.out.println(radius * radius * 3.14);
  }
}
```

※System.out.println()はrailsでのputsにあたる

- 型推論について
宣言と同時に初期値を代入する場合は、省略することも可能
```Java
var 変数名 = 値
```

```Java
class Main {
  public static void main(String[] args) {
    var radius = 5
    System.out.println(radius * radius * 3.14);
  }
}
```
