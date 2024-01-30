# README
Docker_toy_app_caramelcorn

このプロジェクトは、Dockerコンテナ内で動作するRailsアプリケーションを構築するためのものです。以下は、MacでのDockerのインストール手順と、アプリケーションのセットアップ手順です。

Dockerのインストール（Mac）
MacでDockerをインストールするには、Homebrewを使用します。以下の手順に従ってインストールしてください。

Homebrewのインストール: Homebrewがインストールされていない場合は、ターミナルで以下のコマンドを実行してHomebrewをインストールします。

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```
Dockerのインストール: Homebrewを使用してDockerをインストールします。

```
brew install --cask docker
```

Docker Desktopの起動: インストールが完了したら、Docker Desktopが起動するかどうか確認してください。必要に応じて、アプリケーションフォルダからDockerを起動してください。

これで、Mac上でDockerが正常にインストールされました。

アプリケーションのセットアップ
Dockerがインストールされたら、以下の手順でアプリケーションのセットアップを行います。

このプロジェクトをクローンします。
```
git clone https://github.com/ShinichiKikukawa/Docker_toy_app_caramelcorn.git
```

```
cd Docker_toy_app_caramelcorn
```

Dockerコンテナをビルドします。
```
docker build -t toy_app_caramelcorn .
```

Dockerコンテナを実行します。アプリケーションはポート3000でリッスンします。
```
docker run -p 3000:3000 toy_app_caramelcorn
```

これで、Dockerコンテナ内でRailsアプリケーションが実行され、ポート3000でアクセスできるようになります。簡単なセットアップ手順で、アプリケーションを試すことができます。
