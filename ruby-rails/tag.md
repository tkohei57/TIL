# RailsでShare MLBにタグ付け機能を実装する。

## 実装手順
1.モデル・テーブルの作成
2.コントローラー、モデルへ必要な処理を記述
3.ビューで見た目を整える

## モデル・テーブルの作成
- 記事にタグをつけることができるようにするため、tagsテーブルが必要。
- 1つの記事に対して複数のタグをつけることができ、1つのタグは複数の記事につけられることもあるので多対多のアソシエーションを組むために中間テーブルを用意する。
→それぞれのコマンドを実行

1.tagsのマイグレーションファイル
```ruby
class CreateTags < ActiveRecord::Migration[5.2]
  def change
    create_table :tags do |t|
      t.string :name,null: false
      t.timestamps
    end
  end
end

```

2.中間テーブル(article_tags)のマイグレーションファイル
```ruby
class CreateArticleTags < ActiveRecord::Migration[5.2]
  def change
    create_table :article_tags do |t|
      t.references :article, null: false, foreign_key: true
      t.references :tag, null: false, foreign_key: true

      t.timestamps
    end
    # 同じタグを２回保存するのを出来ないようにする
    add_index :article_tags, [:article_id, :tag_id], unique: true
  end
end

```

3.tag.rb
```ruby
class Tag < ApplicationRecord
  has_many :article_tags, dependent: :destroy, foreign_key: 'tag_id'
  has_many :articles, through: :article_tags

  validates :name, uniqueness: true, presence: true
end
```

4.article_tag.rb
```ruby
class ArticleTag < ApplicationRecord
  belongs_to :article
  belongs_to :tag
  
  validates :article_id, presence: true
  validates :tag_id, presence: true
end
```

5.article.rb
```ruby
class Article < ApplicationRecord
  # 省略
  
  has_many :article_tags, dependent: :destroy
  has_many :tags, through: :article_tags
  
  # 省略
end
```

## コントローラー・モデルにタグを保存するためのコードを記述

※今回はフォームオブジェクトパターンを使用せずに実装

1.articles_controller.rb
```ruby
class ArticlesController < ApplicationController

  # 省略

  def create
    @article = Article.new(article_params)
    tag_list = params[:article][:name].split(',') # paramsから入力されたタグを,で区切って配列にし、変数tag_listに代入
    if @article.save
      @article.save_tag(tag_list) # 記事が保存されたら、変数tag_listを引数にしてタグを保存するメソッドを実行
      to_root
    else
      render :new
    end
  end
 
  # 省略
 
end
```

2.article.rb
```ruby
class Article < ApplicationRecord

  # 省略
  
  # タグを保存するメソッドを定義
  def save_tag(sent_tags)
  
    # タグが存在していれば、タグの名前を配列として全て取得
    current_tags = self.tags.pluck(:name) unless self.tags.nil?  # pluckメソッドは、引数に指定したカラムの値を配列で返してくれるメソッド
    
    # 先ほど取得したタグから送られてきたタグを除いてold_tagsとする(不要なタグ)
    old_tags = current_tags - sent_tags
    
    # 送信されてきたタグから現在存在するタグを除いたタグをnew_tagsとする(新たなタグ)
    new_tags = sent_tags - current_tags
  
    # 古いタグを消す
    old_tags.each do |old|
      self.tags.delete Tag.find_by(name: old)
    end
  
    # 新しいタグを保存
    new_tags.each do |new|
      new_article_tag = Tag.find_or_create_by(name: new) # find_or_create_byメソッドは引数の条件に該当するデータがあればそれを返し、なければ新規作成後保存(create)する。
      self.tags << new_article_tag # その記事に紐づくタグとして追加されていく
    end
  end
end
```

## ビューの調整
1._article.html.erb
```ruby
<div class="article-tags-area">
  <i class="fa-solid fa-tags tag-icon"></i><%= article.tags.map(&:name).join(', ') %>
</div>
```

2._post.html.erb
```ruby
<div class="article-tags">
  <%= f.text_field :name, value: @tag_list, class: "tag-form", placeholder: '","で区切ってタグを入力' %>
  <!-- value: @tag_listは編集機能で必要になるためのコード -->
</div>
```

3.show.html.erb
```ruby
<div class="show-article-tags">
  <i class="fa-solid fa-tags tag-icon"></i><%= @article_tags.map(&:name).join(', ') %>
</div>
```

## 参考にした記事
- [[Ruby on rails]タグ付け機能① 複数のタグ付け](https://qiita.com/ki_87/items/a344ea566c88b10b950c)
