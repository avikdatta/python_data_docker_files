FROM resin/armv7hf-debian-qemu


RUN [ "cross-build-start" ]

USER root
ENV NB_USER pi
ENV NB_UID 1000

RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER 
USER $NB_USER
WORKDIR /home/$NB_USER

RUN git clone https://github.com/yyuu/pyenv.git ~/.pyenv

USER root
RUN [ "cross-build-end" ]
USER $NB_USER
