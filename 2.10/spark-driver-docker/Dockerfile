FROM anchormen/spark:1.6.1_2.10

MAINTAINER Mohamed ElSioufy <m.sioufy@anchormen.nl>

COPY app.jar /opt/app.jar

CMD /opt/spark/bin/spark-submit --class $SPARK_CLASS --master spark://master:7077 /opt/app.jar
