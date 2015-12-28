FROM debian

RUN apt-get update &&\
    apt-get install -y curl git-core &&\
    curl -sL https://deb.nodesource.com/setup | bash - &&\
    apt-get update &&\
    apt-get install -y nodejs

RUN apt-get update &&\
    apt-get install -y build-essential

RUN adduser ethnetintel

RUN cd /home/ethnetintel &&\
    git clone https://github.com/cubedro/eth-net-intelligence-api &&\
    cd eth-net-intelligence-api &&\
    npm install &&\
    npm install -g pm2

WORKDIR /home/ethnetintel/eth-net-intelligence-api
RUN chown -R ethnetintel /home/ethnetintel/eth-net-intelligence-api

ADD start /start
RUN chmod +x /start

USER ethnetintel
ENTRYPOINT ["/start"]
