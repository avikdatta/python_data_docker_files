FROM resin/armv7hf-debian-qemu
MAINTAINER reach4avik@yahoo.com
ENTRYPOINT []

USER root
ENV NB_USER pi
ENV NB_UID 1000

WORKDIR /root/

RUN [ "cross-build-start" ]

RUN apt-get  update &&   \
    apt-get install -y   \
    autoconf             \
	build-essential      \
	ca-certificates      \
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
    gfortran              

RUN apt-get purge -y python.*

RUN locale-gen en_US.UTF-8
RUN dpkg-reconfigure locales

RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER 

RUN [ "cross-build-end" ]

USER $NB_USER
WORKDIR /home/$NB_USER

RUN git clone https://github.com/yyuu/pyenv.git ~/.pyenv

RUN mkdir -p tmp           
ENV TMPDIR=/home/$NB_USER/tmp
ENV PYENV_ROOT="/home/$NB_USER/.pyenv"   
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
        picamera
        
CMD ["jupyter-notebook","--ip","0.0.0.0"]
