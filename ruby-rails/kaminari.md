# Gem kaminariを使用してページネーションを行う（Share MLBでの実装）

## kaminariのインストール
1.Gemfileに以下を記入
```ruby
gem 'kaminari'
```

2.ターミナルでbundle installを実行
```
bundle install
```

## ページネーションの実装
1.articles_controller.rbのindexアクションに以下のコードを記述
```ruby
def index
  @articles = Article.includes(:user)
  @articles = Article.page(params[:page]).per(5).order('created_at DESC')
end
```
2.ページネーションを実装したいビューファイル内に以下のコードを記述
```ruby
<%= paginate @articles %>
```
