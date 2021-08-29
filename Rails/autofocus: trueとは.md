## autofocus属性とは
「autofocus: true」とはページを読み込んだらすぐにautofocus属性を記述している部分にカーソルが移動して入力状態になる記述。

```
 <div class="form-field-name">
  <%= f.text_field :name, autofocus: true %>
 </div>
```
