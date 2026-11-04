# Primera etapa: obtener un JDK completo de Java 8
FROM eclipse-temurin:8-jdk AS jdk

# Segunda etapa: imagen Hadoop con Sqoop
FROM apache/hadoop:3.4.0

USER root

# Incorporar el JDK
COPY --from=jdk /opt/java/openjdk /opt/java/openjdk

ENV JAVA_HOME=/opt/java/openjdk
ENV HADOOP_HOME=/opt/hadoop
ENV SQOOP_HOME=/opt/sqoop

ENV PATH=$JAVA_HOME/bin:$SQOOP_HOME/bin:$HADOOP_HOME/bin:$PATH

COPY sqoop-1.4.7.tar.gz /tmp/
COPY mysql-connector-j-8.0.33.jar /tmp/

RUN tar -xzf /tmp/sqoop-1.4.7.tar.gz -C /opt/ \
    && mv /opt/sqoop-1.4.7.bin__hadoop-2.6.0 /opt/sqoop \
    && cp /tmp/mysql-connector-j-8.0.33.jar /opt/sqoop/lib/ \
    && rm -f /tmp/sqoop-1.4.7.tar.gz /tmp/mysql-connector-j-8.0.33.jar

ENV HADOOP_COMMON_HOME=/opt/hadoop
ENV HADOOP_MAPRED_HOME=/opt/hadoop
ENV HADOOP_HDFS_HOME=/opt/hadoop
ENV HADOOP_YARN_HOME=/opt/hadoop

WORKDIR /opt/sqoop

CMD ["bash"]