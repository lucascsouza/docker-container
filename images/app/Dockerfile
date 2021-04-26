FROM php:7.3-apache

RUN apt-get update && apt-get install -y git zip unzip libxml2-dev

RUN docker-php-ext-install mysqli pdo pdo_mysql

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"
RUN echo 'error_reporting = E_ALL'              > "$PHP_INI_DIR/conf.d/error_reporting.ini" && \
    echo 'display_errors = On'                  > "$PHP_INI_DIR/conf.d/display_errors.ini" && \
    echo 'html_errors = On'                     > "$PHP_INI_DIR/conf.d/html_errors.ini" && \
    echo 'display_startup_errors = On'          > "$PHP_INI_DIR/conf.d/display_startup_errors.ini" && \
    echo 'post_max_size = 150M'                 > "$PHP_INI_DIR/conf.d/post_max_size.ini" && \
    echo 'upload_max_filesize = 150M'           > "$PHP_INI_DIR/conf.d/upload_max_filesize.ini" && \
    echo 'date.timezone = "America/Sao_Paulo"'  > "$PHP_INI_DIR/conf.d/date.timezone.ini"

# composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php --filename=composer --install-dir=/usr/bin && \
    php -r "unlink('composer-setup.php');"
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_DISABLE_XDEBUG_WARN 1

# APACHE MOD REWRITE
RUN a2enmod rewrite

COPY entrypoint.sh /usr/bin/entrypoint
RUN chmod +x /usr/bin/entrypoint

EXPOSE 80 443