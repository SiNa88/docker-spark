# Spark docker
Docker images to:
* Setup a standalone [Apache Spark](https://spark.apache.org/) cluster running one Spark Master and multiple Spark workers
* Build Spark applications in Java, Scala or Python to run on a Spark cluster

Currently version:
* Spark 3.1.1 for Hadoop 2.7.0 with OpenJDK 8
* Spark Driver should be installed with python 3.9 as the spark executor uses python 3.9

## Using Docker Compose
```sh
$ sudo bash build.sh
$ sudo docker-compose up &
```
