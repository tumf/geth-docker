FROM quay.io/tumf/gvm
MAINTAINER y.takahara@gmail.com

# Configurations
ENV GO_VERSION 1.5.1
ENV GETH_GIT_REPO https://github.com/ethereum/go-ethereum.git
ENV GETH_GIT_TAG v1.4.10

# Usual update / upgrade
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN apt-get upgrade -q -y
RUN apt-get dist-upgrade -q -y

# Let our containers upgrade themselves
RUN apt-get install -q -y unattended-upgrades

# Install Go
RUN bash -c "source /root/.gvm/scripts/gvm &&\
    gvm install go${GO_VERSION} &&\
    gvm use go${GO_VERSION} --default"

# Install geth
RUN apt-get install -y build-essential libgmp3-dev
RUN bash -c "source /root/.gvm/scripts/gvm &&\
    cd /tmp &&\
    git clone ${GETH_GIT_REPO} &&\
    cd go-ethereum/ &&\
    git pull --tags &&\
    git checkout refs/tags/${GETH_GIT_TAG} &&\
    make geth &&\
    install -m 755  build/bin/geth /usr/bin/"

EXPOSE 8545
EXPOSE 30303

VOLUME /data

ADD password /password
ADD start /start
RUN chmod +x /start
ENTRYPOINT ["/start"]
