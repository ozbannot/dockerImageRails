# dockerImageRails

## 環境
・Docker<br>
※ Docker Desktopをinstall<br>
https://docs.docker.com/desktop/

## 構成
```
◆アプリケーション構成群
・DB
・Buildinserver
・Ruby
◆Docker-compose.yml(アプリケーション構成群記述ファイル)
◆src(アプリケーション格納場所)
```

## 構成スペック
```
・DB
- MySQL v8
・Ruby
- v2.7
・Rails
- v6.1
```

## 環境構築
```
① git clone {this repository} cd {this repository}

② docker compose up -d --build

③ docker-compose run web rails db:create(テスト用DB作成)

```

## アクセス
```
http://127.0.0.1:3000/
```

## Dockerコマンド
```
・Dockerfileの書き換えなどのビルド処理の変更をイメージに反映させる
docker-compose up --build
・イメージを元にコンテナを起動する(Dockerfileの変更がなければこっちでOK)
docker-compose up
・option -d
デタッチ、バックグラウンド起動
・コンテナを落とす
docker-compose down
・テスト用DB作成（これをしないとappが表示されない）
docker-compose run web rails db:create
downさせてpsを切ったりするとupする際にもう一度上記のコマンドでDBを作り直す必要がある
```

## herokuに本番デプロイ
```
注意：M1 Macbookの場合、上記のコンテナイメージだとherokuに本番デプロイする際にハマる（heroku側のMySQLの問題でマシンイメージをlinux/amd64に対応させる必要あり）
解決する際に参考したサイト：https://zenn.dev/daku10/articles/m1-heroku-container-trouble-exec-format-error
上記のコンテナイメージを参考にさらにherokuデプロイ用のコンテナイメージを作成するイメージ
```
```
当時の実行コマンド(参考)
・currentディレクトリからheroku対応用のイメージを作り直す
docker buildx build . --platform linux/amd64 -t {username}/{appname}:latest
・タグ作成
docker tag {username}/{appname} registry.heroku.com/{appname}/web
・heroku対応用のイメージ作成
docker push registry.heroku.com/{appname}/web
・イメージ確認
docker images
・herokuにコンテナデプロイ
heroku container:release web -a {appname}
・db作成（オプション）※今回こけた元の原因
heroku run bundle exec rake db:migrate RAILS_ENV=production -a {appname}
・app公開
heroku open
```


