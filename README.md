# README
# Docker_toy_app_caramelcorn

このプロジェクトは、Dockerコンテナ内で動作するRailsアプリケーションを構築するためのものです。以下は、MacでのDockerのインストール手順と、アプリケーションのセットアップ手順です。

## Dockerのインストール（Mac）
MacでDockerをインストールするには、Homebrewを使用します。以下の手順に従ってインストールしてください。
※homebrew経由でなく、公式からダウンロードすることはお勧めしません。何らかの原因でdocker自体を再インストールする必要があった時、アンインストールしたとしてもファイルが残ってしまう可能性が捨て切れないからです。
あくまで、パッケージ管理ツールを適切に使うことをお勧めします。

### Homebrewのインストール: Homebrewがインストールされていない場合は、ターミナルで以下のコマンドを実行してHomebrewをインストールします。

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```
### Dockerのインストール: Homebrewを使用してDockerをインストールします。

```bash
brew install --cask docker
```

Docker Desktopの起動: インストールが完了したら、Docker Desktopが起動するかどうか確認してください。必要に応じて、アプリケーションフォルダからDockerを起動してください。

これで、Mac上でDockerが正常にインストールされました。

## アプリケーションのセットアップ
Dockerがインストールされたら、以下の手順でアプリケーションのセットアップを行います。

### このプロジェクトをクローンします。
```bash
git clone https://github.com/ShinichiKikukawa/Docker_toy_app_caramelcorn.git
```
### チェンジディレクトリします。
```bash
cd Docker_toy_app_caramelcorn
```

### イメージをビルドします。
```bash
docker-compose build
```

### bundle installします。
```bash
docker-compose run --rm web bundle install
```
### yarn installします。
```bash
docker-compose run --rm web yarn install
```
### DBのセットアップを1発で実行します。
```bash
docker-compose run --rm web rails db:create db:migrate db:seed
```
↓※下記と同じことです。
rails db:create
```bash
docker-compose run --rm web rails db:create
```

rails db:migrate
```bash
docker-compose run --rm web rails db:migrate
```

rails db:seed
```bash
docker-compose run --rm web rails db:seed
```

### railsサーバー起動(ローカルPC用)
```bash
bin/dev
```
### 実行権限がないとエラーになったら以下のコマンドを実行して下さい。
```bash
chmod +x bin/dev bin/init bin/end
```

これで、bin/initでドッカーが1発で立ち上がります。また、1発でコンテナを止めて消せます。詳しくは、bin/initとbin/endの処理を見て、十分にご納得の上お使い下さい。bin/devも使えます。同様にbin /devの処理を見てからお使い下さい。

これで、Dockerコンテナ内でRailsアプリケーションが実行され、ポート3000でアクセスできるようになります。簡単なセットアップ手順で、アプリケーションを試すことができます。

bin/initの処理
```
#!/bin/sh

# シェルスクリプトが失敗した場合には、直ちに終了する
set -e;

# イメージのビルド
echo "Building Docker images...";
docker-compose build;

# bundle install
echo "Running bundle install...";
docker-compose run --rm web bundle install;

# yarn installの前にキャッシュをクリア
echo "Clearing Yarn cache...";
docker-compose run --rm web yarn cache clean;

# yarn install
echo "Running yarn install...";
docker-compose run --rm web yarn install --verbose;

# db:create db:migrate db:seed
echo "Setting up the database...";
docker-compose run --rm web rails db:create db:migrate db:seed;

# railsサーバー起動
echo "Starting Rails server...";
bin/dev;

```

bin/endの処理
```
#!/bin/sh

# スクリプトが失敗した場合に直ちに終了する
set -e
# 実行中の全てのドッカーコンテナを停止
echo "Stopping all Docker containers..."
docker stop $(docker ps -aq)

# すべてのドッカーコンテナを削除
echo "Removing all Docker containers..."
docker rm $(docker ps -aq)

echo "All Docker containers have been stopped and removed."

```

bin/devの処理
```
#!/bin/sh
#
# 開発環境を起動する
#
# set-e Doc: https://qiita.com/youcune/items/fcfb4ad3d7c1edf9dc96
set -e;

# server.pidの削除
cat <<EOS
=============================
===== delete server.pid =====
=============================
EOS
rm -f ./tmp/pids/server.pid

# アプリケーションの起動
cat <<EOS
====================================
=== run docker-compose up -it db ===
====================================
EOS
docker-compose up -d db

# railsコンテナだけを一回削除して、railsコンテナを再度立ち上げ、コンテナ内に入りrailsを起動させる（いつも通りデバックができる）
cat <<EOS
========================================
===== railsコンテナを起動中... =====
========================================
EOS
if [ $# == 1 ]; then
  docker-compose run --rm -p $*:3000 web rails s -b 0.0.0.0;
else
  docker-compose run --rm -p 3000:3000 web rails s -b 0.0.0.0;
fi

```
