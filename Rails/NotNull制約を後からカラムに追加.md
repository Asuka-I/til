`rails g migration ChangeColumnsAddNotnullOnテーブル名`を実行

```db.rb
class ChangeColumnsAddNotnullOnSeals < ActiveRecord::Migration[6.1]
  def change
    change_column_null :seals, :prefecture_id, false
    change_column_null :seals, :place, false
  end
end
```
