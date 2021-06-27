## pagenationを使った降順
```ruby:posts_controller.rb
@posts = Post.all.order(created_at: :desc).page(params[:page]).per(PER_PAGE)
```
昇順にする場合は`desc`を`asc`に変える
