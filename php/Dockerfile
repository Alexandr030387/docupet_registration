FROM php:8.1-fpm

# Install necessary build tools
RUN apt-get update && apt-get install -y \
    gcc \
    make \
    autoconf \
    && rm -rf /var/lib/apt/lists/*

# Install required extensions and dependencies
RUN apt-get update && apt-get install -y \
    libbz2-dev \
    libcurl4-openssl-dev \
    libxml2-dev \
    mariadb-client \
    libssl-dev \
    libldap-dev \
    libpcre3-dev \
    libmariadb-dev \
    libonig-dev \
    libpng-dev \
    libjpeg-dev \
    libzip-dev \
    zip \
    unzip \
    libicu-dev \
    libldap2-dev \
    libgd-dev \
    libpq-dev
 # Remove default PHP extensions
RUN docker-php-ext-install -j$(nproc) \
    mysqli \
	pdo_mysql \
    ctype \
    soap \
    session \
    dom
 # Install additional PHP extensions
RUN docker-php-ext-install -j$(nproc) \
    bcmath \
    zip \
    intl \
    gd \
    bz2 \
    mbstring \
    pgsql \
    opcache

COPY --from=composer /usr/bin/composer /usr/bin/composer
WORKDIR /var/www/docupet_registration
EXPOSE 9000
CMD php-fpm
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN curl -sS https://get.symfony.com/cli/installer | bash