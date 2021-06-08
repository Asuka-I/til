# 既存データベースにカラムを追加

  1: rails g migration Addカラム名Toテーブル名 カラム名:データ型
  2: [例]　rails g migration AddImageToFoods image:string

マイグレーションファイルが下記のように追加される

   1: class AddImageToFoods < ActiveRecord::Migration[6.1]
   2:  def change
   3:    add_column :foods, :image, :string
   4:  end
   5: end

カラムを変更や追加などを行った時は、必ず

rails db:migrate

を行う！

❯ rails db:migrate                              
== 20210608120028 AddImageToFoods: migrating ==================================
-- add_column(:foods, :image, :string)
   -> 0.0236s
== 20210608120028 AddImageToFoods: migrated (0.0236s) =========================

上記になれば成功。
