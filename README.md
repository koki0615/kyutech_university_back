## container

laravel 開発環境構築

├── app<br>
├── web<br>
└── db<br>

**app container**<br>

- Base image<br>
  - php:8.1-fpm-buster<br>
  - composer:2.2

**web container**<br>

- Base image<br>
  - nginx:1.20-alpine

**db container**<br>

- Base image<br>
  - mysql/mysql-server:8.0

## 環境構築方法

Laravel の環境を構築したいディレクトリで `git clone` を行い、フォルダを作成する。
docker compose.yml ファイルがあるディレクトリで以下のコマンドを順に打つ

1. `docker compose build` コマンドでイメージ作成
2. `docker compose up -d` コマンドでコンテナを作成し、バックグラウンドで実行
3. `docker compoes exec app bash` コマンドで app コンテナに入る
4. `chmod -R 777 storage bootstrap/cache` コマンドで書き込み権限を付与
5. `composer install` コマンドで vendor ディレクトリへライブラリ群をインストール
6. .env ファイルが見当たらない場合は.env.example ファイルが生成されているので、.env に名前を変更する
7. `php artisan key:generate` コマンドでアプリケーションキーを作成
8. `php artisan storage:link` 　コマンドでシンボリックリンクを張る
9. `php artisan serve` コマンドで laravel の環境構築が完成

おまけ  
`docker compoes exec app bash` コマンドで app コンテナに入り、  
`php artisan migrate` コマンドを打つと、db との接続が確認できる。  
エラーが出る場合は、  
infra→mysql→Dockerfile の環境変数と src→vendor→.env の環境変数が等しいか、  
.env ファイルの DB_HOST が自分の db コンテナの名前と等しいか確認してみてください。
