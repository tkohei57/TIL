# Javaにおけるメソッドについて

## mainメソッドとは？
mainメソッド

1.ファイルを実行するとmainメソッドが実行される

2.mainメソッドの引数などは、必ず決められた通りに記述する必要がある

例
```Java
class Main {
  public static void main(String[] args) {  
      // ここに処理を書く
  {
}
```

## メソッドの定義方法
- 書き方
```Java
アクセス修飾子 static修飾子 返り値のデータ型　メソッド名() {
  // 行いたい処理
}
```

- アクセス修飾子
→外部への公開範囲を設定するためのものでpublic, private, protectedの3種類存在する。publicにする必要がないものは、極力privateを使用した方が良い。

※クラスや変数の公開範囲を設定するために使うこともできる。

- static修飾子
→staticをつけることで「静的メソッド」として定義される。静的メソッドは、「クラスメソッド」とも呼ばれ、rubyにおけるクラスメソッドとほぼ同じ。

※staticを付けない場合は、「インスタンスメソッド」として定義される

- 返り値のデータ型
→メソッドが実行された結果返される返り値のデータ型をあらかじめ指定しておく必要がある。

※返り値が合い場合はvoidを指定する。

## メソッドの実行
例
```Java
class Main {
  public static void main(String[] args) {
    var answer = square(5);
    System.out.println(answer);
  }

  public static int square(int number){
    return number * number;
  }
}

// 処理の流れ　
// ①ファイルが読み込まれることで自動的にmainメソッドが実行される。
// ②変数answerに引数で5を与えたsquareメソッドが実行された結果が代入される（上の例では5*5の結果である25が代入される）。
//　　※squareメソッドは引数に数値が与えられ、その引数同士の掛け算が行われた結果を数値で返すメソッド。
//　　③変数answerに代入されている25が出力される。
```
