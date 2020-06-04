
```sh
# fix permission problem to accesss docker sock
# https://www.digitalocean.com/community/questions/how-to-fix-docker-got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket
sudo groupadd docker
sudo usermod -aG docker $USER
# log out and login
su -s ${USER}
docker login quay.io

docker build -t ubuntu-aarch64 .
```
