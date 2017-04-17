# A Dockerfile for running PySpark on Jupyter

## Build image

<pre><code>
git clone https://github.com/avikdatta/python_data_docker_files.git

docker build -t pi-pyspark-notebook python_data_docker_files/pi-pyspark-notebook/
</code></pre>

## Run Pyspark with Jupyter

<pre><code>
docker run -it -p 4040:4040                  \
               -p 8888:8888                  \
               -v /path:/home/pi/path        \
               --net=host                    \
               pi-python-data:spark-jupyter5 \
               bash -c "export YARN_CONF_DOR='/home/pi/app/hadoop-2.7.3/etc/hadoop';jupyter-notebook --ip 0.0.0.0"

</code></pre>

## Create Spark context for local scheduler

* Open Jupyter link in browser
* Create new notebook
* Create Spark context
<pre><code>
from pyspark import SparkConf, SparkContext
conf=SparkConf().setMaster('local').setAppName("My App")
sc=SparkContext(conf=conf)
</code></pre>

## Create Spark context for yarn

* Open Jupyter link in browser
* Create new notebook
* Import Yarn conf
<pre><code>
import os
os.environ['YARN_CONF_DIR']='/path/hadoop-2.7.3/etc/hadoop/'
</pre></code>

* Create Spark context
<pre><code>
from pyspark import SparkConf, SparkContext
conf=SparkConf().setMaster('yarn-client').setAppName("My App").set('spark.executor.memory','128m').set('spark.memory.fraction','0.1').set('spark.memory.useLegacyMode','true').set('spark.yarn.am.memory','128m')
sc=SparkContext(conf=conf)
</pre></code>
