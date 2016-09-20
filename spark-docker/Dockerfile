FROM debian:8.5


MAINTAINER m.sioufy@anchormen.nl


####installing [software-properties-common] so that we can use [apt-add-repository] to install Java8
RUN apt-get update -y \
&&  apt-get install software-properties-common -y \
&&  echo "deb http://ftp2.fr.debian.org/debian/ unstable main contrib non-free" >> /etc/apt/sources.list \
&&  echo "deb http://ftp2.fr.debian.org/debian/ testing main contrib non-free" >> /etc/apt/sources.list \
&&  echo "deb http://ftp2.fr.debian.org/debian/ stable main contrib non-free" >> /etc/apt/sources.list

####installing java and supervisor
RUN apt-get update -y \
&&  apt-get install -y openjdk-8-jre-headless supervisor wget


####downloading & unpacking Spark 1.6.1 [prebuilt for Hadoop 2.6+ and scala 2.10]
RUN wget http://apache.crihan.fr/dist/spark/spark-1.6.1/spark-1.6.1-bin-hadoop2.6.tgz \
&&  tar -xzf spark-1.6.1-bin-hadoop2.6.tgz \
&&  mv spark-1.6.1-bin-hadoop2.6 /opt/spark

#RUN hadoop fs -mkdir /opt/spark/logs/spark-events
#RUN mkdir -p /opt/spark/logs/spark-events


#####adding conf files [to be used by supervisord for running spark master/slave]
COPY master.conf /opt/conf/master.conf
COPY slave.conf /opt/conf/slave.conf
COPY log4j.properties /opt/spark/conf/log4j.properties


#######exposing port 8080 for spark master UI
EXPOSE 8080
EXPOSE 7077

#default command: running an interactive spark shell in the local mode
CMD ["/opt/spark/bin/spark-shell", "--master", "local[*]"]
