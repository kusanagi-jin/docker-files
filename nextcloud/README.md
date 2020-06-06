# nextcloud 19

based on https://github.com/nextcloud/docker/blob/0599d1022cc4e1192a19f1c8fcd83c6d195d6b96/19.0/apache/Dockerfile


## build

```
sudo docker build ./nextcloud -t nextcloud19:v1

sudo docker tag nextcloud19:v1 docker.pkg.github.com/kusanagi-jin/footloose-images/nextcloud19:v1

sudo docker push docker.pkg.github.com/kusanagi-jin/footloose-images/nextcloud19:v1
```

## run

```
docker run -d -p 8080:80 docker.pkg.github.com/kusanagi-jin/footloose-images/nextcloud19:v1
```
