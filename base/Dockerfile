FROM ubuntu:16.04

MAINTAINER Anshul Jindal <anshul.jindal@tum.de>

ENV ENABLE_INIT_DAEMON true
ENV INIT_DAEMON_BASE_URI http://identifier/init-daemon
ENV INIT_DAEMON_STEP spark_master_init

COPY wait-for-step.sh /
COPY execute-step.sh /
COPY finish-step.sh /

#COPY bde-spark.css /css/org/apache/spark/ui/static/timeline-view.css
USER root

# Spark dependencies
ENV APACHE_SPARK_VERSION 3.1.1
ENV HADOOP_VERSION 2.7

RUN apt-get -y update && \
    apt-get install --no-install-recommends -y openjdk-8-jre-headless ca-certificates-java wget && \
    rm -rf /var/lib/apt/lists/*

RUN apt-get update \
 && apt-get install -y curl unzip \
    build-essential libpq-dev libssl-dev openssl libffi-dev zlib1g-dev

RUN apt-get install -y software-properties-common

RUN add-apt-repository ppa:deadsnakes/ppa -y

RUN apt-get update \
 && apt-get install -y python3-pip python3.7-dev python3.7 \
 && ln -s /usr/bin/python3.7 /usr/bin/python \
 && pip3 install py4j \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*


#&& easy_install3 pip py4j \


ENV PYTHONHASHSEED 0
ENV PYTHONIOENCODING UTF-8
ENV PIP_DISABLE_PIP_VERSION_CHECK 1

RUN cd /tmp && \
    wget -q http://mirrors.ukfast.co.uk/sites/ftp.apache.org/spark/spark-${APACHE_SPARK_VERSION}/spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
    echo "5C773553B785B16237DFBE7A39F34BEA6BF1D4E10E520BD27D55B2767E2883DE5A06ACF33447E571570A2D3CC34B5094F15D17BEF81A2AB16080A64F3AB34A0B *spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz" | sha512sum -c - && \
    tar xzf spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz -C /usr/local --owner root --group root --no-same-owner && \
    rm spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz
RUN cd /usr/local && ln -s spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} spark

#
# Spark and Mesos config
ENV SPARK_HOME /usr/local/spark
ENV PYTHONPATH $SPARK_HOME/python:$SPARK_HOME/python/lib/py4j-0.10.7-src.zip
ENV MESOS_NATIVE_LIBRARY /usr/local/lib/libmesos.so
ENV SPARK_OPTS --driver-java-options=-Xms1024M --driver-java-options=-Xmx4096M --driver-java-options=-Dlog4j.logLevel=info

#Give permission to execute scripts
RUN chmod +x /wait-for-step.sh && chmod +x /execute-step.sh && chmod +x /finish-step.sh
