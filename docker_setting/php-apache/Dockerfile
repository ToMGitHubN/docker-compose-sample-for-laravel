# [START dockerfile]
FROM php:7.4.7-apache-buster

# install PHP拡張モジュール + vim + node
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash - \
	&& apt-get install -y wget libjpeg-dev libfreetype6-dev \
	&& apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y libzip-dev libwebp-dev libjpeg-dev libpng-dev libicu-dev libxml2-dev libxslt1-dev zlib1g-dev g++ zip unzip libonig-dev \
	&& apt-get install -y git vim \
	&& apt-get remove cmdtest \
	&& apt-get install -y nodejs \
	&& apt-get install -y libfreetype6-dev \
	&& docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
	&& docker-php-ext-install bcmath calendar exif zip gd gettext intl mysqli pcntl pdo_mysql soap sockets xsl opcache \
	&& pecl install redis \
	&& docker-php-ext-enable redis \
	&& apt-get clean

# mod_rewrite ON
RUN a2enmod rewrite

# DOCUMENT_ROOT change
# Basic認証
ENV APACHE_DOCUMENT_ROOT=/var/www/html/public
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf \
    && sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf
#    && sed -i -e '$a <Location />\nAuthType Basic\nAuthName "Basic Auth"\nAuthUserFile /var/www/html/.htpasswd\nRequire valid-user\n</Location>' /etc/apache2/apache2.conf


# LANGUAGE ja_JP.UTF-8
RUN apt-get install -y locales \
	&& apt-get clean \
	&& locale-gen ja_JP.UTF-8 \
	&& localedef -f UTF-8 -i ja_JP ja_JP
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:jp
ENV LC_ALL ja_JP.UTF-8

# install composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && chmod +x /usr/local/bin/composer




# [END dockerfile]
