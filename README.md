# env-docker-laravel

## 使い方

1. env ファイルをコピー `cp example.env .env`
1. イメージビルド `docker compose build`
1. 指定バージョンのララベルをインストール `docker compose run --rm app composer create-project laravel/laravel:^{version} ./`
1. docker-compose.yml の volumes に関するところをコメント解除
1. docker 起動 `docker compose up -d`
1. vendor インストール `docker exec app composer install`
1. node modules インストール `docker exec app npm install`
1. vite 開発サーバ起動 `docker exec app npm run dev`

## ブランチ

| name       | role                                                       | 派生元 | マージ先 |
| ---------- | ---------------------------------------------------------- | ------ | -------- |
| master     | 公開するものを置くブランチ                                 |        |          |
| base       | laravel のバージョン選択ができるところで止まってるブランチ | master | master   |
| v{version} | laravel バージョンごとのブランチ                           | base   |          |
