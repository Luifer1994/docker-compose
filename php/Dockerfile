FROM php:8.2-fpm

# Establecer directorio de trabajo
WORKDIR /var/www/html

# Instalar dependencias del sistema
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    libzip-dev \
    unixodbc-dev \
    libgssapi-krb5-2 \
    libssl-dev \
    gnupg \
    unixodbc

# Instalar la extensión zip
RUN docker-php-ext-install zip

# Descargar el controlador MYSQL ODBC
#RUN curl -L https://dev.mysql.com/get/Downloads/Connector-ODBC/8.0/mysql-connector-odbc-8.0.26-linux-glibc2.12-x86-64bit.tar.gz -o mysql-connector-odbc-8.0.26-linux-glibc2.12-x86-64bit.tar.gz

# Instalar las extensiones MYSQL
#RUN docker-php-ext-install pdo_mysql mysqli && docker-php-ext-enable mysqli
# Limpiar cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Instalar extensiones de PHP 
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

# Obtener el último Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Copiar shell scripts
COPY scripts /var/www/salescontrol/php

# Eliminar caracteres incompatibles
RUN sed -i 's/\r$//' /var/www/salescontrol/php/*.sh

# Otorgar permisos de ejecución a los archivos sh
RUN chmod +x /var/www/salescontrol/php/*.sh

RUN echo "upload_max_filesize = 100M" >> /usr/local/etc/php/php.ini && \
    echo "post_max_size = 100M" >> /usr/local/etc/php/php.ini


CMD ["/var/www/salescontrol/php/run.sh"]
