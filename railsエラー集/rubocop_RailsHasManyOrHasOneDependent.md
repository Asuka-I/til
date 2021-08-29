## Rails/HasManyOrHasOneDependent

```
Rails/HasManyOrHasOneDependent: Specify a :dependent option.
  has_many :worships
  ^^^^^^^^
```

## 解決方法

- userと一緒にpostsを削除
  - Tableを削除したときの関連itemsオブジェクトをどう扱うのかというのを定義
  - `:destroy`
  - `:delete_all`

- userだけ削除する（postsは削除しない）
  - `:nullify`

今回は下記を指定
```
class User < ApplicationRecord

  has_many :worships, dependent: :destroy
end
```

## 参考

https://qiita.com/takayuu276/items/b86ac6b620d2b15c0164
