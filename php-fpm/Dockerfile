#FROM php:7.4-fpm-alpine

## Install Node, NVM, NPM and Grunt
#
#RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
#  	&& apt-get install -y nodejs build-essential \
#    && curl https://raw.githubusercontent.com/creationix/nvm/v0.16.1/install.sh | sh \
#    && npm i -g grunt-cli yarn

RUN apk update && apk add git

RUN set -x \
      && apk add --no-cache ca-certificates \
      && apk add --no-cache --virtual build-dependencies go git musl-dev \
      && mkdir -p /opt/go \
      && export GOPATH=/opt/go \
      && go get github.com/mailhog/mhsendmail
# Install Composer
RUN curl -sL https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
   && composer --version

ADD config/php.ini $PHP_INI_DIR/

RUN chmod 777 -Rf /var/www /var/www/.*
VOLUME /var/www/html
WORKDIR /var/www/html
CMD ["php-fpm", "-F"]
