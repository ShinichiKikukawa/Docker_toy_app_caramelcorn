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


これで、Dockerコンテナ内でRailsアプリケーションが実行され、ポート3000でアクセスできるようになります。簡単なセットアップ手順で、アプリケーションを試すことができます。
