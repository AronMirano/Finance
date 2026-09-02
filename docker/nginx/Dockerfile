FROM php:8.4-fpm

WORKDIR /var/www/gfms
ENV TZ=Asia/Manila

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update  && apt-get install -y curl  zip  unzip
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install pdo pdo_mysql

COPY --from=composer/composer:latest-bin /composer /usr/bin/composer

RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

# Copy existing application directory permissions
COPY --chown=www:www . /var/www/gfms

# Change current user to www
USER www
EXPOSE 9000

CMD ["php-fpm"]
