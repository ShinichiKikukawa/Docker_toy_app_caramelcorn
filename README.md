# README.md
# Docker_toy_app_caramelcorn

このプロジェクトは、Dockerコンテナ内で動作するRailsアプリケーション(7.1.3)、ruby(3.2.2)を構築するためのトイアプリです。以下は、MacでのDockerのインストール手順と、アプリケーションのセットアップ手順です。キャラメルコーンに深い意味はありません。甘くて美味しいイメージのアプリです。プラスのイメージが大切です。苦手意識を一緒に克服しましょう。

## 想定する開発者
macユーザー※windouwsは詳しくないので省略させていただきます。
rails学習初心者
docker未使用者またはdocker初心者
dockerに苦手意識がある方

## DockerとRailsのバージョン互換性
このプロジェクトは、以下のDockerとRailsのバージョンでテストされています。
- Docker: バージョン 20.10.21 (他のバージョンでも動作する可能性がありますが、このバージョンでの動作が確認されています)
- Rails: 7系(7.1.3)

異なるバージョンを使用する場合は、特にDockerのインストールや設定において、互換性の問題が生じる可能性があるため、公式ドキュメントを参照し、必要に応じて設定を調整してください。

## プロジェクトの構成とアーキテクチャ

このプロジェクトは、以下の主要なコンポーネントから構成されています：

- **アプリケーションのディレクトリ構造**:
  - `app/`: アプリケーションの主要なビジネスロジックが含まれています。
  - `config/`: アプリケーションの設定ファイルが含まれています。
  - `db/`: データベースのマイグレーションとスキーマが含まれています。

- **使用される主要な技術**:
  - Rails: アプリケーションのバックエンドフレームワーク。
  - Docker: 開発とデプロイメントのためのコンテナ化技術。

- **データベースの設計**:
  - データベースはRailsのActive Recordを利用して管理されます。
  - `schema.rb` ファイルでデータベースのスキーマを確認できます。

## オープンソースプロジェクトとしてのポテンシャル
- 当プロジェクトは、オープンソースコミュニティにおける教育的および実験的なツールとしての大きな可能性を秘めています。初心者や学習者にとって、このトイアプリは以下のような多様な利点を提供します：

- 技術的な概念の探求: 本プロジェクトを通じて、RailsやDockerなどの最新技術の実装と概念を探求することができます。
- コミュニティとの協力: オープンソースプロジェクトとして、他の開発者と協力し、新たなアイデアや改善を共有することが可能です。
継続的な成長と進化: コミュニティからのフィードバックを取り入れ、プロジェクトをより成熟したアプリケーションへと発展させることができます。
- トイアプリとしての活用
このプロジェクトは、実験的なアイデアや新技術のテストベッドとして理想的です。その主な利用方法は以下の通りです：

- 新技術の試験: 新しいライブラリやフレームワークを安全な環境で試すことができます。
- コンセプトの検証: 新しいアイデアを実装し、その実現可能性をテストします。
このプロジェクトは、ただのトイアプリを超え、教育的なリソースおよびオープンソースコミュニティにとって価値ある貢献となることを目指しています。

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

### which dockerで自分のPCのどこにインストールされたか、念のため確認しておきましょう。
```bash
which docker
```
### docker -vでバージョンを念のため確認しておきましょう。
```bash
docker -v
```

### docker-compose -vでインストールされているか、またバージョンを念のため確認しておきましょう。
```bash
docker-compose -v
```
インストールされていなければ、以下に進みます。

### docker-composeのダウンロード
macの場合
ターミナルで、docker-composeの1.29.2のバージョンをインストールします。
```bash
sudo curl -L https://github.com/docker/compose/releases/download/1.29.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```

### docker-composeのコマンドに実行権限を付与します。
```bash
sudo chmod +x /usr/local/bin/docker-compose
```
### docker-composeのバージョンを確認します。
```bash
docker-compose -v
```
### 以下のように表示されたら成功です。
docker-compose version 1.29.2, build 5becea4c

※ただし、Docker ComposeはDocker Desktop for Macに含まれている場合が多いので、別途インストールする必要がない場合もあります​。docker-compose -vで適切に表示されていれば、このトイアプリでは問題ありません。

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

### 実行権限を付与します。以下のコマンドを実行して下さい。(bin/init等はカスタムスクリプトです。一連の環境構築コマンド群をひとまとめにしてあります。)
```bash
chmod +x  bin/init bin/end bin/dev
```

### bin/initのコマンドを打って1発で立ち上げます。
```bash
bin/init
```

### bin/endのコマンドを打って1発でコンテナを止めて綺麗にします。
```bash
bin/end
```

これで、bin/initでDocker環境がコマンド1発で立ち上がります。また、1発でコンテナを止めて消せます。詳しくは、bin/initとbin/endの処理を見て、十分にご納得の上お使い下さい。bin/devも使えます。同様にbin/devの処理を見てからお使い下さい。

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

※以下のように一つ一つ実行しても立ち上がります。
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

## よくあるエラーと対処法
- **エラー: Dockerコンテナが起動しない**
  - 対処法: Docker Desktopが正常に起動しているか確認し、必要に応じてDocker Desktopを再起動してください。

- **エラー: `docker-compose`コマンドが見つからない**
  - 対処法: Docker Composeが正しくインストールされているかを確認し、必要に応じてインストールしてください。

- **エラー: データベースのマイグレーションに失敗する**
  - 対処法: `docker-compose run --rm web rails db:migrate`コマンドを再度実行してみてください。エラーメッセージを確認し、具体的な問題を解決してください。

- **何らかの混在が生じて、dockerがうまく起動しない**
  - 対処法: docker desktopの右上の"虫"のアイコンをクリックし、Reset to factory defaultsのボタンをクリックして、イメージ、ボリューム、コンテナを全て消してしまいます。(十分ご納得の上実施してください。)その後、再トライします。

<img width="1440" alt="スクリーンショット 2024-01-31 3 40 08" src="https://github.com/ShinichiKikukawa/Docker_toy_app_caramelcorn/assets/107759288/994ca434-db96-49d0-88f6-e3b29f06e94b">


これらのエラーは一般的なものであり、多くの場合、上記の対処法で解決可能です。しかし、それでも問題が解決しない場合は、プロジェクトのissueトラッカーで問題を報告してください。


## コントリビューションガイド

このプロジェクトへの貢献に興味がある方のためのガイドラインです：

- **貢献の方法**:
  - GitHubのIssueトラッカーを使用してバグを報告したり、機能リクエストを提出します。
  - Pull Requestを通じてコードの貢献を行います。

- **バグ報告とフィーチャーリクエスト**:
  - クリアで詳細な説明を提供してください。
  - 可能であれば、問題を再現するためのステップを含めてください。

- **コードレビューのプロセス**:
  - 提出されたPull Requestは、プロジェクトのメンテナによってレビューされます。
  - コードの品質、スタイルガイドへの遵守、テストの実施が考慮されます。


更新日時
2023/1/31
※最新の情報を提供するよう心がけていますが、古くなっていたら、ご連絡ください。
