# env-docker-laravel

## 使い方

### base ブランチからバージョン指定で laravel をインストール

1. env ファイルをコピー `cp example.env .env`
1. イメージビルド `docker compose build`
1. 指定バージョンのララベルをインストール `docker compose run --rm app composer create-project laravel/laravel:^{version} ./`
1. docker-compose.yml の volumes に関するところをコメント解除
1. laravel 配下, docker-compose.yml を v{version}ブランチにコミット
1. docker 起動 `docker compose up -d`
1. vendor インストール `docker compose exec app composer install`
1. node modules インストール `docker compose exec app npm install`
1. vite 開発サーバ起動 `docker compose exec app npm run dev`

### バージョンブランチから　 laravel を起動

1. 使いたいバージョンのブランチをチェックアウト
1. env ファイルをコピー `cp example.env .env`
1. イメージビルド `docker compose build`
1. docker 起動 `docker compose up -d`
1. vendor インストール `docker compose exec app composer install`
1. node modules インストール `docker compose exec app npm install`
1. vite 開発サーバ起動 `docker compose exec app npm run dev`

## ブランチ

| name       | role                                                       | 派生元 | マージ先 |
| ---------- | ---------------------------------------------------------- | ------ | -------- |
| master     | latest バージョンのララベルがインストールされてる          |        |          |
| base       | laravel のバージョン選択ができるところで止まってるブランチ | master | master   |
| v{version} | laravel バージョンごとのブランチ                           | base   |          |
