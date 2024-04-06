FROM phpdockerio/php73-fpm:latest
WORKDIR "/application"

# RUN mkdir -p /run/php-fpm \
#     && chown -R user:user /run/php-fpm
# RUN useradd -m user \
#     && echo "user:password" | chpasswd
# USER user

# Создаем пользователя и группу
RUN groupadd -g 1000 user && \
    useradd -u 1000 -g user -m user

# Меняем владельца для нужного каталога
RUN mkdir -p /run/php-fpm && \
    chown -R user:user /run/php-fpm


# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install  php7.3-pgsql php7.3-gd php-redis \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install git
RUN apt-get update \
    && apt-get -y install git \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*