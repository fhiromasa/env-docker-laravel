FROM php:8.1-apache

# Composerのインストール
COPY --from=composer:lts /usr/bin/composer /usr/bin/composer

# ミドルウェアインストール
# https://hub.docker.com/_/php/
RUN apt-get update && \
  apt-get install --no-install-recommends -y \
    # dev library
    libpq-dev libonig-dev libxml2-dev libzip-dev \
    # SMTP デーモンの代わりを果たしてくれる
    msmtp msmtp-mta \
    # GD で使う画像処理系ライブラリ
    libfreetype6-dev  libjpeg62-turbo-dev  libpng-dev \
    # node
    nodejs npm && \
  docker-php-ext-configure gd --with-freetype --with-jpeg && \
  docker-php-ext-install -j$(nproc) gd && \
  docker-php-ext-install pdo pdo_mysql mysqli zip

# mod_rewriteを有効化する
RUN a2enmod rewrite

# タイムゾーン設定
RUN ln -sf  /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# PHP 設定ファイル
# COPY php.ini /etc/php.ini
COPY php.ini /usr/local/etc/php/php.ini

# apache 設定
COPY apache2/apache2.conf /etc/apache2/apache2.conf
COPY apache2/sites-available/000-default.conf /etc/apache2/sites-available/000-default.conf

#smtp 設定
COPY msmtprc /etc/msmtprc

WORKDIR /var/www/laravel/

CMD ["apache2-foreground"]
