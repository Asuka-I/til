初期データを生成してくれるファイルのこと。

テストデータを作成の際によく使う。
``` seeds.rb
ActiveRecord::Base.connection.execute("TRUNCATE TABLE users RESTART IDENTITY CASCADE")
ActiveRecord::Base.connection.execute("TRUNCATE TABLE posts RESTART IDENTITY CASCADE")

user1 = User.create!(email: "satou@example.com", password: "password")
user2 = User.create!(email: "suzuki@example.com", password: "password")
user3 = User.create!(email: "tanaka@example.com", password: "password")

Post.create!(content: "おはよう", user_id: user2.id)
Post.create!(content: "こんにちは", user_id: user3.id)
Post.create!(content: "こんばんは", user_id: user3.id)

puts "初期データの投入に成功しました！"
```

記述が終わったら必ず、`rails db:seed`を実行する。
