FROM ubuntu:16.04
MAINTAINER reach4avik@yahoo.com

ENTRYPOINT []

ENV NB_USER vmuser
ENV NB_GROUP vmuser
ENV NB_UID 1000

USER root
WORKDIR /root/

RUN apt-get -y update &&   \
    apt-get install -y     \
    git                    \
    locales                \
    wget                   \
    make                   \
    g++                    \
    patch                  \
    build-essential        \
    libssl-dev             \
    zlib1g-dev             \
    libbz2-dev             \
    libsqlite3-dev         \
    libssl-dev             \
    libreadline6-dev       \
    libreadline6           \
    openssh-server         \
    libopenblas-dev        \
    mysql-client-5.7       \
    libmysqlclient-dev     \
    graphviz               \
    golang                 \
    libhtml-template-perl  \
    libjson-perl           \
    libdbi-perl            \
    libdbd-mysql-perl      \
    libcpan-sqlite-perl    \
    libdbd-sqlite3-perl    \
    libgraphviz-perl       \
    sshfs

RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER && \
    groupadd $NB_GROUP && \
usermod -a -G $NB_GROUP $NB_USER

USER $NB_USER
WORKDIR /home/$NB_USER

RUN git clone https://github.com/Ensembl/ensembl-hive.git && \
    cd ensembl-hive && \
    git checkout master
 
WORKDIR /home/$NB_USER
    
RUN git clone https://github.com/Ensembl/guiHive.git 

ENV EHIVE_ROOT_DIR=/home/$NB_USER/ensembl-hive
ENV PERL5LIB=/home/$NB_USER/ensembl-hive/modules:$PERL5LIB

RUN cd /home/$NB_USER/guiHive && \
    git checkout server && \
    bash guihive-deploy.sh && \
    cd server && \
    go build

EXPOSE 3306
EXPOSE 8080

CMD [ 'guiHive/server/server' ]
