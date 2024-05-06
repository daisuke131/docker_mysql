# docker_mysql

## docker起動

Makefileを作成しているので下記コマンドで起動できる。

```
$ make up
```

↓で止める。

```
$ make down
```

## rails設定

rails new
gemfileのみ書き換える(y)

```
$ bundle exec rails new . -d mysql --api --skip-bundle --skip-test
```

bundle install

```
# 1回目
$ bundle install --path=vendor/bundle --jobs=4
# 2回目以降
$ bundle install --local --path=vendor/bundle --binstubs=vendor/bin --jobs=4
```

database.yml修正

```
default: &default
  adapter: mysql2
  encoding: utf8mb4
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password:
  host: '127.0.0.1' # ←ここだけ修正
```

データベース作成

```
$ bundle exec rails db:create
```

rails起動

```
$ bundle exec rails s -b 0.0.0.0
```

.gitignore追記

```
vendor/bundle
vendor/bin
```
