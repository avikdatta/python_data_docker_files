FROM resin/rpi-raspbian:jessie-20161026
MAINTAINER reach4avik@yahoo.com

USER root
WORKDIR /root/

RUN apt-get -y update && \
    apt-get install -y   \
    git                  \
    locales              \
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

RUN pip install    \
        cython     \
        ipython    \
        numpy      \
        scipy      \
        sklearn    \
        pandas     \
        pymysql    \
        matplotlib \
        seaborn    \
        jupyter
        
