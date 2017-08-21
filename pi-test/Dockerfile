FROM resin/armv7hf-debian-qemu

RUN [ "cross-build-start" ]

USER root
ENV NB_USER pi
ENV NB_UID 1000

RUN apt-get update && apt-get install -y git 

RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER 
USER $NB_USER
WORKDIR /home/$NB_USER

RUN set -x \
    && mkdir -p  /home/$NB_USER/.pyenv

USER root
RUN [ "cross-build-end" ]
USER $NB_USER
