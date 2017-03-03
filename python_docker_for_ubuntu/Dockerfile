FROM ubuntu:16.04
MAINTAINER reach4avik@yahoo.com

RUN apt-get -y update &&                          \
    apt-get install software-properties-common && \
    add-apt-repository ppa:webupd8team/java

RUN apt-get -y update &&   \
    apt-get install -y     \
    git                    \
    locales                \
    oracle-java8-installer \
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
    libopenblas-dev        \
    tk-dev                 \
    gfortran               \
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
        jupyter    \
        pandas_datareader  \
        bs4        \
        matplotlib.finance \
        matplotlib.dates   \
        nltk       \
        gensim 
        
        

    
