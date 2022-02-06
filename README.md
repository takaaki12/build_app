# eisan_app
永産システムの開発imagefile


## プロジェクトマネージャーのおしごと


### ⓪別のリポジトリを作成し、ここの5つのファイルをコピー


### ①Dockerfile、docker-compose.yml内のeisan_appの「eisan」部分を、適宜変更


### ②Dockerfileからimageをbuild
作成した5つのファイルを利用してdocker-compose runを実行し、アプリケーションを生成する。(ターミナルを使って実施)
```
docker-compose run web rails new . --force --no-deps --database=mysql
```


### ③web,dbコンテナを立ち上げる
```
docker-compose build
```


### ④データベースの設定と作成
データベースの情報を設定するために、config/database.ymlファイルを変更し、コマンドでDBを作成する。

```# 設定箇所のみ抜粋
default: &default
  adapter: mysql
  encoding: utf8mb4

  <!-- dbコンテナの名前（いつもなら「db」） -->
  host: db
  
  username: mysql
  password: password # docker-compose.ymlのPOSTGRES_PASSWORDで指定した値
  pool: 5
:
:
development:
  <<: *default
  database: eisan_app_development
:
:
test:
  <<: *default
  database: eisan_app_test
```


### ⑤githubにpushして準備完了



## それぞれのおしごと


### ⑥リモートリポジトリからローカルへclone
```
git clone 'url'
```


### ⑦データベースを作成する
```
docker-compose run web rake db:create
```


### ⑧Dockerを起動
```
docker-compose up
```


### ⑨localhostにアクセスしてサーバーとデータベースの稼働確認
「Yay! You're on Rails！」が出れば問題なし！


お疲れ様でしたー！
