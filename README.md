# phpinfo

## Download app repo

git clone https://github.com/academiaonline/phpinfo
cd phpinfo
git checkout main

## Set common env variables

set ENTRYPOINT=/usr/bin/php
set CMD='-f src/index.php -S 0.0.0.0:8080'

## Run as php app

${ENTRYPOINT} ${CMD}

## Run as Docker container

set IMAGE=phpinfo:0.0.1

docker image build -t ${IMAGE} .

_Pongo . aunque no necesito build context ya que el Dockerfile no utiliza recursos locales para generar la imagen. Uso .dockerignore para ignorar los recursos locales._

docker container run -d --name phpinfo --entrypoint ${ENTRYPOINT} --restart always -v ${PWD}/src/index.php:/src/index.php:ro -p 8080:8080 ${IMAGE} ${CMD}

docker container run -d --name phpinfo --entrypoint /usr/bin/php --restart always -v ${PWD}/src/index.php:/src/index.php:ro -p 8080 phpinfo:0.0.1 -f src/index.php -S 0.0.0.0:8080

## Test

curl localhost:8080/src/index.php
