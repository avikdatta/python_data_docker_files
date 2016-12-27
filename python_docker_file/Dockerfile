FROM resin/rpi-raspbian:jessie-20161026
MAINTAINER reach4avik@yahoo.com

RUN apt-get -y update && \
    apt-get install -y   \
    git                  \
    locales              \
    oracle-java8-jdk     \
    wget                 \
    make                 \
    g++                  \
    patch                \
    build-essential      \
    libssl-dev           \
    zlib1g-dev           \
    libbz2-dev           \
    libsqlite3-dev       \
    libssl-dev           \
    libreadline6-dev     \
    libreadline6         \
    libopenblas-dev      \
    tk-dev               \
    gfortran             \
    mysql-client

WORKDIR /root/
RUN git clone https://github.com/yyuu/pyenv.git ~/.pyenv

RUN mkdir -p tmp           
ENV TMPDIR=/root/tmp
ENV PYENV_ROOT="/root/.pyenv"   
ENV PATH="$PYENV_ROOT/libexec/:$PATH" 
ENV PATH="$PYENV_ROOT/shims/:$PATH" 

RUN locale-gen en_US.UTF-8
RUN dpkg-reconfigure locales

RUN eval "$(pyenv init -)" 
RUN pyenv install 3.5.2
RUN pyenv global 3.5.2

RUN pip install \
        cython  \
        ipython \
        numpy   \
        scipy   \
        sklearn \
        pandas  \
        pymysql
        
RUN wget https://github.com/arq5x/bedtools2/releases/download/v2.26.0/bedtools-2.26.0.tar.gz
RUN tar -xvzf bedtools-2.26.0.tar.gz && \
    cd bedtools2 && \
    make
    
ENV PATH="/root/bedtools2/bin:$PATH" 
RUN pip install pybedtools
    
