FROM resin/rpi-raspbian:jessie-20161026
MAINTAINER reach4avik@yahoo.com

# Run as ROOT
USER root

ENV NB_USER pi
ENV NB_GROUP supergroup
ENV NB_UID 1000

RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER && \
    groupadd $NB_GROUP && \
    usermod -a -G $NB_GROUP $NB_USER

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
    oracle-java8-jdk

RUN locale-gen en_US.UTF-8
RUN dpkg-reconfigure locales

# RUN as the pi user
USER $NB_USER

WORKDIR /home/$NB_USER

ENV APACHE_SPARK_VERSION 2.1.0
ENV HADOOP_VERSION 2.7

RUN cd /home/$NB_USER && \
    git clone https://github.com/yyuu/pyenv.git ~/.pyenv && \
    mkdir -p tmp

ENV TMPDIR=/home/$NB_USER/tmp
ENV PYENV_ROOT="/home/$NB_USER/.pyenv"
ENV PATH="$PYENV_ROOT/libexec/:$PATH"
ENV PATH="$PYENV_ROOT/shims/:$PATH"

# Install Python 2.7.13 and packages
RUN eval "$(pyenv init -)"
RUN pyenv install 2.7.13
RUN pyenv global 2.7.13

RUN pip install    \
        cython     \
        ipython    \
        numpy      \
        scipy      \
        sklearn

RUN pip install    \
        pandas     \
        matplotlib \
        seaborn    \
        jupyter

# Install Apache Spark v 2.1.0
RUN wget -q http://d3kbcqa49mib13.cloudfront.net/spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
    tar -xzf spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
    rm spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
    ln -s spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} spark


EXPOSE 8888
EXPOSE 4040

# Spark config
ENV SPARK_HOME /home/$NB_USER/spark
ENV PYTHONPATH $SPARK_HOME/python:$SPARK_HOME/python/lib/py4j-0.10.4-src.zip
ENV SPARK_OPTS --driver-java-options=-Xms1024M --driver-java-options=-Xmx4096M --driver-java-options=-Dlog4j.logLevel=info
ENV PATH $PATH:$SPARK_HOME/bin

# Enable these two options for creating automatic Spark context while launching jupyter
# ENV PYSPARK_DRIVER_PYTHON "jupyter-notebook"
# ENV PYSPARK_DRIVER_PYTHON_OPTS "--ip 0.0.0.0"
