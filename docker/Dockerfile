
FROM php:5.5-apache

RUN echo "Europe/London" > /etc/timezone && \
    dpkg-reconfigure -f noninteractive tzdata

# Install PHP extension dependencies (if any)
RUN apt-get update 
# RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -

RUN apt-get install -y libpng-dev nodejs-dev nodejs npm

RUN npm install -g less@2.6.0

# RUN apt-get install -y zlib1g-dev libicu-dev g++ libcurl4-gnutls-dev libpng-dev libxml2-dev
#   apt-get -y --no-install-recommends install <package_name>

# Copy PHP configuration
# Edit docker/php.ini and customize it to your needs
COPY docker/php.ini /usr/local/etc/php/php.ini

# Copy custom command docker-php-pecl-install
COPY docker/docker-php-pecl-install /usr/local/bin/

# Install PHP extensions
# RUN docker-php-ext-install mysql
# RUN docker-php-ext-install mysqli
# RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_mysql

# RUN docker-php-ext-install cli
#RUN docker-php-ext-install intl
#RUN docker-php-ext-install curl
#RUN docker-php-ext-install mbstring
RUN docker-php-ext-install gd
#RUN docker-php-ext-install zip
#RUN docker-php-ext-install xml
#RUN docker-php-ext-install dom
# RUN docker-php-ext-install pdo_mysql

# Install PECL extensions
#RUN docker-php-pecl-install <package_name-version> (versions available in PECL repository allowed)

# If you are using XDebug, this might be useful, if not, ignore it
# You additionally will have to customize docker/xdebug-ini-overrides.ini file to your needs
#RUN docker-php-pecl-install xdebug-2.5.4
#COPY docker/xdebug-ini-overrides.ini /usr/local/etc/php/conf.d/docker-php-pecl-xdebug.ini

# Configure Apache VHOSTS
#COPY docker/mysite.com.conf /etc/apache2/sites-available/mysite.com.conf
#RUN a2ensite <mysite.com.conf>

# Activate Apache modules
RUN a2enmod rewrite
RUN a2enmod expires
RUN a2enmod headers
RUN service apache2 restart

# Set the workdir
WORKDIR /var/www/html