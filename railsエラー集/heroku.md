以下のエラーが発生
```
heroku config
  Error: Missing required flag:
  -a, --app APP  app to run command against
  See more help with --help
```

herokuと紐付けられていない様だった
```
git remote -v
origin  git@github.com:example.git (fetch)
origin  git@github.com:example.git (push)
```
## 解決方法

以下を実行
```
heroku git:remote -a アプリ名
```
または
```
heroku git:create アプリ名
```
```
https://サブドメイン.herokuapp.com/ | https://git.heroku.com/サブドメイン.git
```

以下のコマンドで確認できる
```
heroku config | grep HEROKU_APP_NAME
HEROKU_APP_NAME: アプリ名
```
