# Ruby 3.0 buster for arm64

based on ruby buster and  https://github.com/CircleCI-Public/circleci-dockerfiles



## build

```
sudo docker build ./ -t dron-buster-ruby:3.0.0-preview1

sudo docker tag dron-buster-ruby:3.0.0-preview1 docker.pkg.github.com/kusanagi-jin/docker-files/dron-buster-ruby:3.0.0-preview1

sudo docker push docker.pkg.github.com/kusanagi-jin/docker-files/dron-buster-ruby:3.0.0-preview1
```

