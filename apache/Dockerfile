FROM php:apache

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN apt-get update && apt-get upgrade -y && apt-get install nano wget libpq-dev libzip-dev unzip libfreetype6-dev libjpeg62-turbo-dev libpng-dev -y && \
docker-php-ext-install bcmath pdo_pgsql pdo_mysql exif zip && docker-php-ext-enable exif && \
docker-php-ext-install -j$(nproc) iconv && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && docker-php-ext-install -j$(nproc) gd \
&& a2enmod rewrite

RUN chmod -R 777 /var/www/html && rm /etc/localtime && ln -s /usr/share/zoneinfo/America/Bahia /etc/localtime && echo "America/Bahia" > /etc/timezone && \
sed "s/;date.timezone =/date.timezone = America\/Bahia/g" /usr/local/etc/php/php.ini-development  > /usr/local/etc/php/php.ini


EXPOSE 80 9000
