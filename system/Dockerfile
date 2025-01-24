FROM php:8.2.27-cli

WORKDIR /code

RUN apt update

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --no-ansi --install-dir=/usr/bin --filename=composer
RUN composer --ansi --version --no-interaction
RUN php --ini
RUN apt-get install libzip-dev -y
RUN apt-get install zip unzip -y
RUN apt upgrade -y
RUN php -r "unlink('composer-setup.php');"

COPY suple_ti/ .

RUN composer install

RUN apt install -y nodejs npm

RUN npm install --legacy-peer-deps
RUN npm install vue-loader@^16.2.0 --save-dev --legacy-peer-deps
