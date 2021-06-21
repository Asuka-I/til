# アプリを作成した際にすべきこと*.gitignoreの追記*

## `.DS_Store`を追記
```
# 以下を追加
.DS_Store
/vendor/bundle

# RubyMineを使用されている方は次も追加
/.idea
```

## なぜすべきか

- 不要なファイルをGitHubにプッシュしない為
  - vendor/bundle が入っている状態で bundle install すると200mb以上もの不要なgemデータなどがプッシュされることになる。
- 共有するメリットがない
- 無駄なコンフリクトを起こす可能性がある
