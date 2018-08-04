FROM php:7.2-apache

RUN set -ex; \
	\
	apt-get update; \
	apt-get install -y \
		libjpeg-dev \
		libpng-dev \
        # for xmlrpc extension
        libxml2-dev \
        # for intl extension
        libicu-dev \
	; \
	rm -rf /var/lib/apt/lists/*; \
	\
	docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr; \
	docker-php-ext-install gd mysqli opcache zip xmlrpc soap intl

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=2'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
		echo 'post_max_size=2048M'; \
		echo 'upload_max_filesize=2048M'; \
	} > /usr/local/etc/php/conf.d/opcache-recommended.ini

RUN a2enmod rewrite expires

# Install XDebug
# Enable and configure xdebug
#RUN pecl install xdebug-2.5.0
#RUN docker-php-ext-enable xdebug
#RUN { \
#		echo 'xdebug.remote_enable=1'; \
#		echo 'xdebug.remote_handler=dbgp'; \
#		echo 'xdebug.remote_port=9000'; \
#		echo 'xdebug.remote_autostart=1'; \
#		echo 'xdebug.remote_connect_back=0'; \
#		echo 'xdebug.remote_connect_back=0'; \
#		echo 'xdebug.idekey=PHPSTORM'; \
#		echo 'xdebug.remote_host=192.168.56.1'; \
#	} >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

VOLUME /var/www/html

# Data directory.
RUN mkdir /var/www/data
RUN chown www-data:www-data /var/www/data
VOLUME /var/www/data

# Composer cache location for www-data user.
# RUN mkdir /var/www/.composer
# RUN chown www-data:www-data /var/www/.composer
# VOLUME /var/www/.composer

# PHPUnit.
# RUN mkdir /var/www/phpunit
# RUN chown www-data:www-data /var/www/phpunit
# VOLUME /var/www/phpunit

# Behat.
# RUN mkdir /var/www/behat
# RUN chown www-data:www-data /var/www/behat
# VOLUME /var/www/behat

# Install locale we need for PHPUnit.
# Set the locale
RUN apt-get clean && apt-get update
RUN apt-get install -y locales
RUN echo 'en_AU.UTF-8 UTF-8' >> /etc/locale.gen
RUN locale-gen

CMD ["apache2-foreground"]
