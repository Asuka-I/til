## ActionView::Template::Error
#### ログイン済みのユーザーがログアウトすると、下記のようなエラーが発生。

ActionView::Template::Error (undefined method `id' for nil:NilClass):
```
    3:   <p>【食品名】<%= food.name %></p>
    4:   <p>
    5:     <%= link_to "詳細", food %>
    6:     <% if current_user.id == food.user_id %>
    7:       <%= link_to "編集", edit_food_path(food) %>
    8:       <%= link_to "削除", food_path(food), method: :delete, data: { confirm: "削除しますか？" } %>
    9:     <% end %>
  
app/views/foods/_food.html.erb:6
app/views/foods/index.html.erb:2
```

## 解決方法
該当箇所をみても記述ミスなどが見当たらない。また、ルートやコントローラも問題が見当たらず。  
下記の共通コントローラを再度チェック。

```
    1: class ApplicationController < ActionController::Base
    2:  before_action :authenticate_user! except: :index
    3: end
```

`except: :index` を削除したところ解消した。

## 参考
https://pikawaka.com/rails/before_action#exceptオプション

#### お問い合わせ画面のリンクをクリックした際に下記のエラーが発生

```
ActionView::Template::Error (undefined method `submitted' for nil:NilClass):
    1: <h1>お問い合わせ<%= " 《確認》" if @contact.submitted == "1" %></h1>
    2: <%= form_with model: @contact, local: true do |form| %>
    3:   <%= render "error_messages", form: form %>
    4:   <%= form.hidden_field :submitted %>
```

## 解決方法
contacts_controllerの
```
  def index
    @contacts = Contact.new
  end
```
を下記に変更
```
  def index
    @contact = Contact.new
  end
```
