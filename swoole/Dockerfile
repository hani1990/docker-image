FROM koolob/swoole-docker
COPY sources.list /etc/apt/sources.list
ENV TZ Asia/Shanghai
RUN apt-get update && apt-get install -qqy \
        libmcrypt-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
        libmemcached-dev \
        libicu-dev

RUN docker-php-ext-install -j$(nproc) mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install intl mysqli pdo_mysql opcache bcmath

WORKDIR /opt
VOLUME ["/opt"]

CMD php ./examples/app_server.php start && tail -f ./tmp/log/swoole.log

EXPOSE 8991 9501 8888 80