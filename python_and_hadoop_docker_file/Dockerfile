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
    gfortran    

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
        pandas

RUN wget http://www.mirrorservice.org/sites/ftp.apache.org/hadoop/common/hadoop-2.7.3/hadoop-2.7.3.tar.gz 

RUN tar xvzf hadoop-2.7.3.tar.gz

RUN JAVA=$(readlink -f /usr/bin/java | sed 's:jre/bin/java::')
ENV JAVA_HOME=${JAVA}
ENV HADOOP_INSTALL=/root/hadoop-2.7.3
ENV PATH=$PATH:$HADOOP_INSTALL/bin
ENV PATH=$PATH:$HADOOP_INSTALL/sbin
ENV HADOOP_MAPRED_HOME=$HADOOP_INSTALL
ENV HADOOP_COMMON_HOME=$HADOOP_INSTALL
ENV HADOOP_HDFS_HOME=$HADOOP_INSTALL
ENV YARN_HOME=$HADOOP_INSTALL
ENV HADOOP_HOME=$HADOOP_INSTALL

