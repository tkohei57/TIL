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
## 日本語表記化
config/locales内にkaminari_ja.ymlを作成し、以下のコードを記述
```ruby
ja:
  views:
    pagination:
      first: "&laquo; 最初"
      last: "最後 &raquo;"
      previous: "&lsaquo; 前"
      next: "次 &rsaquo;"
      truncate: "..."
  helpers:
    page_entries_info:
      one_page:
        display_entries:
          zero: ""
          one: "<strong>1-1</strong>/1件中"
          other: "<strong>1-%{count}</strong>/%{count}件中"
      more_pages:
        display_entries: "<strong>%{first}-%{last}</strong>/%{total}件中"
```
