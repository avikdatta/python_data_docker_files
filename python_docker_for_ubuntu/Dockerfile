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
    libopenblas-dev        \
    tk-dev                 \
    gfortran               \
    mysql-client-5.7       \
    sqlite3                \
    r-base                 \
    r-base-dev             \
    libsqlite3-dev
    
RUN locale-gen en_US.UTF-8
RUN dpkg-reconfigure locales

RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER && \
    groupadd $NB_GROUP && \
usermod -a -G $NB_GROUP $NB_USER

USER $NB_USER
WORKDIR /home/$NB_USER

RUN git clone https://github.com/yyuu/pyenv.git ~/.pyenv

RUN mkdir -p /home/$NB_USER/tmp          
ENV TMPDIR=/home/$NB_USER/tmp
ENV PYENV_ROOT="//home/$NB_USER/.pyenv"   
ENV PATH="$PYENV_ROOT/libexec/:$PATH" 
ENV PATH="$PYENV_ROOT/shims/:$PATH" 



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
        matplotlib \
        seaborn    \
        jupyter    \
        pandas_datareader  \
        bs4        \
        matplotlib \
        nltk       \
        gensim     \
        pymysql    \
        xlrd       \
        openpyxl   \
        sqlalchemy \
        slackclient \
        asana
        
RUN R CMD BATCH "install.packages('devtools')"
RUN R CMD BATCH "devtools::install_github('IRkernel/IRkernel')"
RUN R CMD BATH "IRkernel::installspec()"
     
CMD ["bash"]
