rails db:migrateを実行した際、下記のエラーを検出
```
rails aborted!
StandardError: An error has occurred, this and all later migrations canceled:

'Worship' has no association called 'likes_count'
```
### 解決方法

```
t.integer "likes_count", default: 0
```
の `default: 0` を忘れていたので、追記する。
