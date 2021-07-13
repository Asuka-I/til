`git push heroku HEAD `を実行の際に以下のエラーが発生

```ターミナル.md
Running: rake assets:precompile
rake aborted!
NoMethodError: undefined method `[]' for nil:NilClass
/tmp/build_4c17685f/config/initializers/mail.rb:10:in `<main>'
ーーーーー略ーーーーー
Tasks: TOP => environment
(See full trace by running task with --trace)
 Precompiling assets failed.
 
Push rejected, failed to compile Ruby app.

Push failed

Warning - The same version of this code has already been built: 239fa....

We have detected that you have triggered a build from source code with version 239fa....
at least twice. One common cause of this behavior is attempting to deploy code from a different branch.

If you are developing on a branch and deploying via git you must run:

     git push heroku <branchname>:main

 This article goes into details on the behavior:
   https://devcenter.heroku.com/articles/サブドメイン

 Verifying deploy...

      Push rejected to サブドメイン.

To https://git.heroku.com/サブドメイン.git
 ! [remote rejected] HEAD -> master (pre-receive hook declined)
error: failed to push some refs to 'https://git.heroku.com/サブドメイン.git'
```

```
NoMethodError: undefined method `[]' for nil:NilClass
/tmp/build_4c17685f/config/initializers/mail.rb:10:in `<main>'
```

上記のエラーが出ていたので、`config/initializers/mail.rb`の10行目を確認。

```mail.rb
1.if Rails.env.production?
2.  host = "サブドメイン名.herokuapp.com"
3.  # メール配信に失敗した場合にエラーを発生
4.  ActionMailer::Base.raise_delivery_errors = true
5.  ActionMailer::Base.delivery_method = :smtp
6.  ActionMailer::Base.default_url_options = { host: host }
7.  ActionMailer::Base.smtp_settings = {
8.    port: 587,
9.    address: "smtp.gmail.com",
10.    user_name: Rails.application.credentials.gmail[:address],
11.    password: Rails.application.credentials.gmail[:password],
12.    domain: host,
13.    authentication: "plain"
14.  }
15.end
```

特にタイポなど見られなかった為、以下のファイルを確認
```config/credentials.yml.enc
#gmail:
#  address: アプリ用に作成したメールアドレス
#  password: 16桁のアプリパスワード
```

#がつき、コメントアウトの状態になっていた。以下を修正。
```config/credentials.yml.enc
gmail:
  address: アプリ用に作成したメールアドレス
  password: 16桁のアプリパスワード
```

変更後、再度pushを試みるが、エラーが出る。

今度は以下を実行
```
 RAILS_ENV=production bin/rails assets:precompile
```
エラーは特に発生せず、、、

## 解決方法

ファイルを修正した後、
```
git add .
git commit -m "comment"
```

を実行し、再度pushしてエラー解消！
