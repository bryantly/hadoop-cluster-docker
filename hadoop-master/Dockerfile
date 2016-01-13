FROM hadoop-base

MAINTAINER KiwenLau <kiwenlau@gmail.com>

# move all confugration files into container
ADD files/* /tmp/
ADD http://mirrors.hust.edu.cn/apache/hive/hive-1.2.1/apache-hive-1.2.1-bin.tar.gz /opt/
RUN ln -s /opt/apache-hive-1.2.1-bin /opt/hive

ENV HADOOP_INSTALL /opt/hadoop
ENV SPARK_INSTALL /opt/spark

RUN mkdir -p ~/hdfs/namenode && \ 
mkdir -p ~/hdfs/datanode && \
mkdir $HADOOP_INSTALL/logs

RUN mv /tmp/hdfs-site.xml $HADOOP_INSTALL/etc/hadoop/hdfs-site.xml && \ 
mv /tmp/core-site.xml $HADOOP_INSTALL/etc/hadoop/core-site.xml && \
mv /tmp/mapred-site.xml $HADOOP_INSTALL/etc/hadoop/mapred-site.xml && \
mv /tmp/yarn-site.xml $HADOOP_INSTALL/etc/hadoop/yarn-site.xml && \
mv /tmp/slaves $HADOOP_INSTALL/etc/hadoop/slaves && \
mv /tmp/start-hadoop.sh ~/start-hadoop.sh && \
mv /tmp/run-wordcount.sh ~/run-wordcount.sh && \ 
mv /tmp/start-ssh-serf.sh ~/start-ssh-serf.sh && \
mv /tmp/spark-env.sh $SPARK_INSTALL/conf/spark-env.sh && \
mv /tmp/spark-slaves $SPARK_INSTALL/conf/slaves && \
mv /tmp/start-spark.sh ~/start-spark.sh

RUN chmod +x ~/start-hadoop.sh && \
chmod +x ~/start-spark.sh && \
chmod +x ~/run-wordcount.sh && \
chmod +x ~/start-ssh-serf.sh && \
chmod 1777 tmp

# format namenode
RUN /opt/hadoop/bin/hdfs namenode -format

EXPOSE 22 7373 7946 9000 50010 50020 50070 50075 50090 50475 8030 8031 8032 8033 8040 8042 8060 8088 50060 7077 8080 6066 8081

CMD '/root/start-ssh-serf.sh'; 'bash'
