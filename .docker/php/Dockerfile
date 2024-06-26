FROM php:8.2-fpm-alpine

# Copy File Config
COPY ./.docker/php/www.conf /usr/local/etc/php-fpm.d/www.conf

# Use the default production configuration
COPY ./.docker/php/php.ini "$PHP_INI_DIR/php.ini"

# ADD and set Group
RUN addgroup -g 1000 laravel && adduser -G laravel -g laravel -s /bin/sh -D laravel

# Create folder to run
RUN mkdir -p /var/www/html

# Set Profile
RUN chown laravel:laravel /var/www/html

# Work in the specific space
WORKDIR /var/www/html

# Update package index and install necessary packages
RUN apk update && apk add --no-cache \
    icu-dev \
    libintl \
    freetype \
    freetype-dev \
    libjpeg-turbo \
    libjpeg-turbo-dev \
    libpng \
    libpng-dev \
    libwebp \
    libwebp-dev \
    autoconf \
    g++ \
    make    

# Install intl extension
RUN docker-php-ext-configure intl && docker-php-ext-install intl

# Clean up
RUN apk del autoconf g++ make

# Verify installation
RUN php -m | grep intl

RUN docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg \
    --with-webp

RUN NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
    docker-php-ext-install -j${NPROC} gd 

RUN apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev

RUN docker-php-ext-install pdo pdo_mysql

# Copy existing application directory contents
COPY ./src /var/www/html

# Copy existing application directory permissions
COPY --chown=laravel:laravel ./src /var/www/html

# Change current user to www
USER laravel

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]