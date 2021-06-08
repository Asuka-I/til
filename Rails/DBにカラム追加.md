# 既存データベースにカラムを追加

  ```ターミナル
  rails g migration Addカラム名Toテーブル名 カラム名:データ型
  
  [例]　rails g migration AddImageToFoods image:string
  ```

マイグレーションファイルが下記のように追加される

```20210608120028_add_image_to_foods.rb
class AddImageToFoods < ActiveRecord::Migration[6.1]
  def change
    add_column :foods, :image, :string
  end
end
```

カラムを変更や追加などを行った時は、必ず

`rails db:migrate`

を行う！

```ターミナル
❯ rails db:migrate

== 20210608120028 AddImageToFoods: migrating ==================================
-- add_column(:foods, :image, :string)
   -> 0.0236s
== 20210608120028 AddImageToFoods: migrated (0.0236s) =========================
```

上記になれば成功。
