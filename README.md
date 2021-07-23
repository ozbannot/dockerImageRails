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


