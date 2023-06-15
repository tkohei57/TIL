# JavaにおけるアノテーションとThymeleafについて

## アノテーションとは
クラスやメソッドに特別な意味を持たせるための機能。コードの中で@から始まっている部分。

- サンプルコード
```Java
package in.techcamp.firstapp;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller  // ←ココ！
public class PostController {
    @GetMapping("/hello")　　 // ←ココ！
    @ResponseBody　　 // ←ココ！
    public String showhello() {
        return "<h1>Hello World!</h1>";
    }
}
```

1.@Controller
この記述の後に書かれているクラスはコントローラーとして認識される。

2.@GetMapping
ブラウザで入力されたURLと、実行されるメソッドを紐づけるためのアノテーション。railsにおけるルーティングにあたる。
サンプルコードでは、HTTPメソッドがgetであり、"/hello"というパスでリクエストが送られてきた時のルーティングを示している。

3.@ResponseBody
@ResponseBodyは、ブラウザからのリクエストに対して、直接HTMLを返す際に利用するアノテーション。通常あまり使用されることはない。

## テンプレートエンジンの導入
上のサンプルコードにあるような、@ResponseBodyを使用したビューの表示方法は一般的ではない。railsでのERBに当たるようなライブラリであるThymeleafを導入する。
```Java

// 省略

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
    implementation 'org.springframework.boot:spring-boot-starter-thymeleaf' // この１行を追加
}

// 省略

```

## Thymeleafの使い方
1.ビューファイルの準備
src/main/resources/templates内にhtmlファイルを新規作成する。

2.コントローラーから1で用意したビューファイルを読み込めるようにする。
サンプルコードを例として、以下のようにコードを改変する。
- @ResponseBodyに関する記述を削除
- 用意したビューファイルを読み込むための記述に改変

```Java
package in.techcamp.firstapp;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class PostController {
    @GetMapping("/hello")
    public String showHello(){
        return "hello";  // hello.htmlを呼び出している(.htmlは省略可能)
    }
}
```

## Thymeleafで変数を使用する
Railsでコントローラーからビューに変数を渡す場合は、コントローラーでインスタンス変数に値を代入したがJavaのSping Bootの場合は、Model型のオブジェクトを使用する。

- 実装手順
1.コントローラーの引数でModelオブジェクトを受け取る。
→showHelloメソッドの仮引数に「Model model」と指定し、Modelオブジェクトを受け取る。この時、オブジェクトの変数名は、modelとすることが一般的。
```Java
import org.springframework.ui.Model;  // 追加

// 省略

@GetMapping("/hello")
public String showHello(Model model){

    // 省略

}
```
2.Modelオブジェクトに、ビューで表示させたいデータを追加する
→以下のコードでmodelにデータを追加(addAttributeが追加を行うためのメソッド)。
```Java
@GetMapping("/hello")
public String showHello(Model model){
    var sampleText = "サンプルテキスト";
    model.addAttribute("sampleText", sampleText);
    return "hello";
}
```

※注意点
- 98行目において、１つ目の引数で、ビューで読み込む際の名称を指定している。ダブルクォーテーションで囲んで文字列として指定しなければならない。
- ２つ目の引数でmodelに追加したいデータを指定。

3.ビューファイルでの表示
→Thymeleafではth:textを使用すると、ブラウザに表示したいテキストを任意の内容に置き換えることができる。
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>Hello World from Thymeleaf!</h1>
<p th:text="${sampleText}"></p> // ←ココ！
</body>
</html>
```
※th:text="${sampleText}"と記述することで、pタグの内容を変数sampleTextに代入されている文字列に置き換えている。

