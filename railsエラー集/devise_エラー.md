rails g devise User　を実行の際、以下のエラーが発生
```
rails aborted!
StandardError: An error has occurred, this and all later migrations canceled:

PG::DuplicateColumn: ERROR:  column "email" of relation "users" already exists
```

エラー文を見ると、どうやらusersテーブルが重複しているようだ。

## 試した事
`rails db:migrate:reset`
```
rails aborted!
ActiveRecord::NoEnvironmentInSchemaError: 

Environment data not found in the schema. To resolve this issue, run: 

        bin/rails db:environment:set RAILS_ENV=development
```
binは一切弄っていないので他に原因がありそう

## 解決方法
- 対象モデルを削除する

$ rails destroy devise user

- 次にテーブルを削除するために、削除用のmigrationファイルを作成する

$ rails g migration drop_table_users（←任意のファイル名で可）

- 作成したmigrationファイルにテーブル削除を記述する

（2016××××××××××_drop_table_users.rb）

class DropTableUsers < ActiveRecord::Migration
　def change
　　drop_table :users
　end
end

- マイグレーション実行

$ rails db:migrate

