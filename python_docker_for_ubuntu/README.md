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
<pre><code>
sudo service docker restart
</code></pre>

for ubuntu > 14.04  
<pre><code>
sudo service docker.io restart  
</code></pre>

* Pull docker image
<pre><code>
docker pull avikdatta/python_data_docker_files
</code></pre>

* Check the available images
<pre><code>
docker images
</code></pre>

* Run Jupyter session
<pre><code>
docker run -v /home/$user:/root/data \
           -p 8888:8888 \
           avikdatta/python_data_docker_files:latest \
           jupyter-notebook \
           --ip 0.0.0.0
</code></pre>

* Access the Jupyter secure session using the IP of the server/ virtual machine. You will need the token for accessing this instance

## Installing new packages

Any new packages/tools can be installed in the docker image using the interactive mode

* Run bash from docker
<pre><code>
docker run -v /home/$user:/root/data \
           -it avikdatta/python_data_docker_files:latest \
           /bin/bash
</code></pre>

* Install any tools using apt-get

* Detach the docker container, use Control+pq

* Get the container id
<pre><code>
docker ps
</code></pre>

* Commit changes using a new tag name
<pre><code>
docker commit $container_id avikdatta/python_data_docker_files:new_feature
</code></pre>

* Kill container
<pre><code>
docker kill $container_id
</code></pre>

* Check the available images
<pre><code>
docker images
</code></pre>

* Run new image 
<pre><code>
docker run -v /home/$user:/root/data -p8888:8888 avikdatta/python_data_docker_files:new_feature jupyter-notebook --ip 0.0.0.0
</code></pre>



