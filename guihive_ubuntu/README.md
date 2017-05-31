[![DockerPulls](https://img.shields.io/docker/pulls/avikdatta/guihive_ubuntu.svg)](https://registry.hub.docker.com/u/avikdatta/guihive_ubuntu/)
[![DockerStars](https://img.shields.io/docker/stars/avikdatta/guihive_ubuntu.svg)](https://registry.hub.docker.com/u/avikdatta/guihive_ubuntu/)
[![DockerStars](https://img.shields.io/docker/automated/avikdatta/guihive_ubuntu.svg)](https://registry.hub.docker.com/u/avikdatta/guihive_ubuntu/)

# A docker image for running guiHive server
An ubuntu 16.04 based docker image containing the compiled [guiHive](https://github.com/Ensembl/guiHive) server.

## Run server

USER: ` vmuser `

Access guihive: ` http://HOST_IP_ADDRESS:8080 `

### Connect to MySQL Hive db

MySQL server should be visible to the docker host

` docker run -p8080:8080 --net=host  avikdatta/guihive_ubuntu /home/vmuser/guiHive/server/server  `


### Connect to SQLite database

A remote directory location containing the sqlite database files can be mounted in the docker container

* Run the docker image in interactive mode
` docker run -p8080:8080 -it --net=host --privileged  avikdatta/guihive_ubuntu /bin/bash `

* Create a directory under $HOME
` mkdir -p ~/hive_sqlite_db_dir `

* Mount remote directory
`  sshfs -o uid=1000,gid=100 remote user@remote_serevr:/path/sqlite_db/ /home/vmuser/hive_sqlite_db_dir/ `

* Run GuiHive server
` /home/vmuser/guiHive/server/server `

Use path of mounted directory as the sqlite url for the guihive, e.g.` "sqlite:////home/vmuser/hive_sqlite_db_dir/test_sqlite_hive.db"  `


