# README
Docker_toy_app_caramelcorn
README
Docker_toy_app_caramelcorn

Dockerのインストール（Mac）

マークダウンのコードブロックにできなかったようですが、以下の手順はMacでDockerをインストールする方法です。

Homebrewのインストール:
まず、Homebrewをインストールしてください。Homebrewがインストールされていない場合は、ターミナルで以下のコマンドを実行します。

bash
Copy code
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
Dockerのインストール:
Homebrewを使用してDockerをインストールします。

bash
Copy code
brew install --cask docker
Docker Desktopの起動:
インストールが完了したら、Docker Desktopが起動するかどうか確認してください。必要に応じて、アプリケーションフォルダからDockerを起動してください。これで、Mac上でDockerが正常にインストールされました。

アプリケーションのセットアップ

Dockerがインストールされたら、以下の手順でアプリケーションのセットアップを行います。

このプロジェクトをクローンします。
bash
Copy code
git clone https://github.com/ShinichiKikukawa/Docker_toy_app_caramelcorn.git
プロジェクトディレクトリに移動します。
bash
Copy code
cd Docker_toy_app_caramelcorn
Dockerコンテナをビルドします。
bash
Copy code
docker build -t toy_app_caramelcorn .
Dockerコンテナを実行します。アプリケーションはポート3000でリッスンします。
bash
Copy code
docker run -p 3000:3000 toy_app_caramelcorn
これで、Dockerコンテナ内でRailsアプリケーションが実行され、ポート3000でアクセスできるようになります。簡単なセットアップ手順で、アプリケーションを試すことができます。
