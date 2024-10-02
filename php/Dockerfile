FROM php:8.1-fpm-alpine

RUN docker-php-ext-install pdo pdo_mysql

# autoriser le super utilissateur a modifier si composer est utilise
ENV COMPOSER_ALLOW_SUPERUSER=1

# obtenir composer en utilsant le multi-stage build
COPY --from=composer:2.4 /usr/bin/composer /usr/bin/composer

# copie du composer.json et composer.lock
COPY ./app/composer.* ./
# installation
RUN composer install --prefer-dist --no-dev --no-scripts --no-progress --no-interaction

# copie de l'application dans le dossier de travail
COPY ./app .

# executer composer dump-autoload --optimize
RUN composer dump-autoload --optimize
