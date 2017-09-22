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
    littler                \
    r-cran-littler         \
    r-base                 \
    r-base-dev             \
    r-recommended          \
    libsqlite3-dev         \
    libssl-dev             \
    libcurl3               \
    libcurl3-gnutls
    

RUN locale-gen en_US.UTF-8
RUN dpkg-reconfigure locales

RUN echo 'options(repos = c(CRAN = "https://cran.rstudio.com/"), download.file.method = "libcurl")' >> /etc/R/Rprofile.site \
    && echo 'source("/etc/R/Rprofile.site")' >> /etc/littler.r \
    && ln -s /usr/share/doc/littler/examples/install.r /usr/local/bin/install.r \
    && ln -s /usr/share/doc/littler/examples/install2.r /usr/local/bin/install2.r \
    && ln -s /usr/share/doc/littler/examples/installGithub.r /usr/local/bin/installGithub.r \
    && ln -s /usr/share/doc/littler/examples/testInstalled.r /usr/local/bin/testInstalled.r \
    && install.r docopt \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds \
    && rm -rf /var/lib/apt/lists/*
    

RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER \
     && groupadd $NB_GROUP \
     && usermod -a -G $NB_GROUP $NB_USER

RUN echo "install.packages(c('repr', 'IRdisplay', 'evaluate', 'crayon', 'pbdZMQ', 'devtools', 'uuid', 'digest'))" > /home/$NB_USER/install.R \
    && echo "devtools::install_github('IRkernel/IRkernel')" >> /home/$NB_USER/install.R  \
    && echo "IRkernel::installspec(user = FALSE)" >> /home/$NB_USER/install.R  

ENV R_LIBS_USER /home/$NB_USER/rlib

RUN mkdir -p /home/$NB_USER/rlib

RUN R CMD BATCH --no-save /home/$NB_USER/install.R
     
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
        
CMD ["bash"]
