# Spark docker
Docker images to:
* Setup a standalone [Apache Spark](https://spark.apache.org/) cluster running one Spark Master and multiple Spark workers
* Build Spark applications in Java, Scala or Python to run on a Spark cluster

Currently version:
* Spark 2.4.3 for Hadoop 2.7.0 with OpenJDK 8
* Spark Driver should be installed with python 3.7 as the spark executor uses python 3.7

## Using Docker Compose
```sh
$ sudo bash build.sh
$ sudo docker-compose up &
```
