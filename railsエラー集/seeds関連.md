シードデータを記入後、`rails db:seed` を実行した際に、
以下のエラーが発生
```
rails aborted!
NoMethodError: undefined method `id' for nil:NilClass
```
user_id カラムが抜けていたため、テーブルに追加したが同じエラーが発生。

## 解決方法
ローカルでユーザーの新規登録を行なっていなかった為、改めて登録した。
