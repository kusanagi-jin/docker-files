FROM ruby:3.0.0-preview1-slim-buster

# make Apt non-interactive
RUN echo 'APT::Get::Assume-Yes "true";' > /etc/apt/apt.conf.d/90drone \
  && echo 'DPkg::Options "--force-confnew";' >> /etc/apt/apt.conf.d/90drone

ENV DEBIAN_FRONTEND=noninteractive

# Make sure PATH includes ~/.local/bin
# https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=839155
# This only works for root. The circleci user is done near the end of this Dockerfile
RUN echo 'PATH="$HOME/.local/bin:$PATH"' >> /etc/profile.d/user-local-path.sh

# man directory is missing in some base images
# https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=863199
RUN apt-get update \
  && mkdir -p /usr/share/man/man1 \
  && apt-get install -y \
  git curl mercurial xvfb apt \
  locales sudo openssh-client ca-certificates tar gzip parallel \
  net-tools netcat unzip zip bzip2 gnupg wget make jq \
  apt-transport-https gnupg2 software-properties-common


# Set timezone to UTC by default
RUN ln -sf /usr/share/zoneinfo/Etc/UTC /etc/localtime

# Use unicode
RUN locale-gen C.UTF-8 || true
ENV LANG=C.UTF-8


# Install Docker

#>    # To install, run the following commands as root:
#>    curl -fsSLO https://download.docker.com/linux/static/stable/x86_64/docker-17.05.0-ce.tgz && tar --strip-components=1 -xvzf docker-17.05.0-ce.tgz -C /usr/local/bin
#>
#>    # Then start docker in daemon mode:
#>    /usr/local/bin/dockerd

RUN set -ex \
  && export DOCKER_VERSION=docker-19.03.12.tgz \
  && DOCKER_URL="https://download.docker.com/linux/static/stable/x86_64/${DOCKER_VERSION}" \
  && curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add - \
  && sudo add-apt-repository "deb [arch=arm64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" \
  && sudo apt update \
  && sudo apt-cache policy docker-ce \
  && sudo apt install docker-ce


# docker compose
RUN sudo curl -L "https://github.com/docker/compose/releases/download/1.23.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose \
  && sudo chmod +x /usr/local/bin/docker-compose

RUN groupadd --gid 3434 drone \
  && useradd --uid 3434 --gid drone --shell /bin/bash --create-home drone \
  && echo 'drone ALL=NOPASSWD: ALL' >> /etc/sudoers.d/50-drone \
  && echo 'Defaults    env_keep += "DEBIAN_FRONTEND"' >> /etc/sudoers.d/env_keep \
  && sudo usermod -aG docker drone

RUN sudo mkdir -p /home/drone/.ssh \
  && sudo chmod 700 /home/drone/.ssh \
  && sudo chown drone:drone /home/drone -R
# BEGIN IMAGE CUSTOMIZATIONS

# END IMAGE CUSTOMIZATIONS

USER drone
ENV PATH /home/drone/.local/bin:/home/drone/bin:${PATH}

CMD ["/bin/sh"]
