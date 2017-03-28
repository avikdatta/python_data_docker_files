[![DockerPulls](https://img.shields.io/docker/pulls/avikdatta/python_data_docker_files.svg)](https://registry.hub.docker.com/u/avikdatta/python_data_docker_files/)
[![DockerStars](https://img.shields.io/docker/stars/avikdatta/python_data_docker_files.svg)](https://registry.hub.docker.com/u/avikdatta/python_data_docker_files/)
[![DockerStars](https://img.shields.io/docker/automated/avikdatta/python_data_docker_files.svg)](https://registry.hub.docker.com/u/avikdatta/python_data_docker_files/)
# Python data analysis on Ubuntu

A Docker image for Python data analysis on Ubuntu 16.04. 
Installed Tools:

    Pyenv
    Python 3.5.2
    Pandas
    Scipy
    Numpy
    Scikit-learn
    Matplotlib
    Seaborn
    Jupyter-notebook
    Pymysql
    Beautiful soup 4

## Setup instructions

I ubuntu installed in virtual box for running the Jupyter notebook sessions. The setup instructions can be find below

* Install docker and docker.io 
* Create docker group
sudo groupadd docker

* Add user to the group docker 
`sudo usermod -aG docker $USER`

* Start docker daemon
`sudo service docker restart`

or 

`sudo service docker.io restart for ubuntu > 14.04 )`

* Pull docker image
`docker pull avikdatta/python_data_docker_files`

* Check the available images
`docker images`

* Run Jupyter session
`docker run -v /home/$user:/root/data -p8888:8888 avikdatta/python_data_docker_files:latest jupyter-notebook --ip 0.0.0.0`

* Access the Jupyter secure session using the IP of the server/ virtual machine. You will need the token for accessing this instance

## Installinh new packages

Any new packages/tools can be installed in the docker image using the interactive mode

* Run bash from docker
`docker run -v /home/$user:/root/data -it avikdatta/python_data_docker_files:latest /bin/bash`

* Install any tools using apt-get

* Detach the docker container, use Control+pq

* Get the container id
`docker ps`

* Commit changes using a new tag name
`docker commit $container_id avikdatta/python_data_docker_files:new_feature`

* Kill container
`docker kill $container_id`

* Check the available images
`docker images`

* Run new image 

`docker run -v /home/$user:/root/data -p8888:8888 avikdatta/python_data_docker_files:new_feature jupyter-notebook --ip 0.0.0.0`




