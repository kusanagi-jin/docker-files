# php + apache

diff with original https://github.com/docker-library/php/tree/master/7.4/buster/apache

sudo apt-get install -y libargon2-0-dev

need to chmod +x for scripts

## build

```
sudo docker build ./php-7.4-apache -t php74-apache:v1

sudo docker tag php74-apache:v1 docker.pkg.github.com/kusanagi-jin/footloose-images/php74-apache:v1

sudo docker push docker.pkg.github.com/kusanagi-jin/footloose-images/php74-apache:v1
```
