FROM docker pull avikdatta/python_data

MAINTAINER reach4avik@yahoo.com

USER root

ENV APACHE_SPARK_VERSION 2.1.0
ENV HADOOP_VERSION 2.7
ENV NR_USER pydata
ENV NR_UID 1000

RUN useradd -m -s /bin/bash -N -u $NR_UID $NR_USER

RUN cd /tmp && \
    wget -q http://d3kbcqa49mib13.cloudfront.net/spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
    tar xzf spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz -C /usr/local && \
    rm spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz

RUN cd /usr/local && \
       ln -s spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} spark

# Spark config
ENV SPARK_HOME /usr/local/spark
ENV PYTHONPATH $SPARK_HOME/python:$SPARK_HOME/python/lib/py4j-0.10.4-src.zip
ENV SPARK_OPTS --driver-java-options=-Xms1024M --driver-java-options=-Xmx4096M --driver-java-options=-Dlog4j.logLevel=info

EXPOSE 8888
WORKDIR /home/$NB_USER/work
USER $NR_USER
