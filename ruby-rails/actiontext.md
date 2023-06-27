# Share MLBにaction textを導入する

## ActionTextに関するマイグレーションファイルの生成
- ターミナルで以下のコマンドを実行
```
% rails action_text:install  //マイグレーションファイルが生成される
% rails db:migrate
```

## モデルファイルにリッチテキストを使用することを宣言する
```
class Article < ApplicationRecord

  //省略

  has_rich_text :contents

　　　　//省略

end
```

## ビューファイルにリッチテキスト適用する
```
<div class="article-contents">
  <%= f.rich_text_area :contents, class: "contents-form", id: "contents-form", placeholder: "本文" %>
</div>
```


