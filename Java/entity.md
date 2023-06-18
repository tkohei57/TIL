# Javaにおいてエンティティを作成してデータベースのテーブルとのやり取りを行うまで
- エンティティとは、データベースと連携する際にデータを格納するためのオブジェクトのこと。
- エンティティには、テーブルの各カラムに対応した変数を用意します(例：id、textというカラムを作ると想定するため、エンティティの変数としてid、textを作成する)。
- Javaのプログラムからデータベースにデータを保存する際も、逆にデータを読み込む際もこのエンティティを使用する。

## エンティティの作成
1.ファイルの作成
firstapp/src/main/java内のプロジェクト名がついたディレクトリに、Javaクラスのファイルを作成する(名前は"作成するテーブル名Entity"とすることが一般的)。

2.エンティティの設定
1で作成したファイル内に以下のコードを記述。
```Java
package プロジェクト名;

public class エンティティ名 {
  
    // データベースのテーブルに含まれる「id」と「text」カラムに対応するようエンティティを作成(テーブルのカラムごとに変数を作成)
    private long id;
    private String text;

    // コンストラクタの設定(全ての変数を初期化するコンストラクタに関する記述)
    public PostEntity(long id, String text) {
        this.id = id;
        this.text = text;
    }
  
　　　　　　　　// ゲッターとセッターの記述(全ての変数のゲッター・セッターに関する記述)
    public long getId() {
        return id;
    }

    public void setId(long id) {
        this.id = id;
    }

    public String getText() {
        return text;
    }

    public void setText(String text) {
        this.text = text;
    }
}
```

※ライブラリを使用することで大きくコードを省略できる。

→上記のコードをLombokというライブラリを使用して、コードを簡略化すると以下のようになる。コンストラクタやゲッター・セッターは直接コードを記述することなく、Lombokを使用するのが一般的。

- build.gradle内に以下のコードを記述してライブラリを使用できるようにする。
```Java
dependencies {
  
    // 省略
  
    compileOnly 'org.projectlombok:lombok'
    annotationProcessor 'org.projectlombok:lombok'
      
    // 省略
      
}
```

- エンティティファイルの中身を以下のように修正
```Java
package プロジェクト名;

import lombok.AllArgsConstructor;
import lombok.Data;

// @AllArgsConstructorは、コンストラクタを自動で生成してくれるアノテーション(「すべての変数を初期化するコンストラクタ」を生成するアノテーション)
@AllArgsConstructor

// @Dataというアノテーションを使用して、ゲッターとセッターの記述を省略
@Data

public class エンティティ名 {
    private long id;
    private String text;
}
```
