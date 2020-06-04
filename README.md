push

```sh
# fix permission problem to accesss docker sock
# https://www.digitalocean.com/community/questions/how-to-fix-docker-got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket

cat ~/GH_TOKEN_DOCKER.txt | docker login docker.pkg.github.com -u kusanagi-jin --password-stdin

sudo docker build ./ubuntu-18.04 -t footloose-ubuntu:v1

sudo docker tag footloose-ubuntu:v1 docker.pkg.github.com/kusanagi-jin/footloose-images/footloose-unbuntu:v1

sudo docker push docker.pkg.github.com/kusanagi-jin/footloose-images/footloose-unbuntu:v1

docker pull docker.pkg.github.com/kusanagi-jin/footloose-images/footloose-unbuntu:v1
```

Use as base image in DockerFile:

```
FROM docker.pkg.github.com/kusanagi-jin/footloose-images/footloose-unbuntu:v1
```
