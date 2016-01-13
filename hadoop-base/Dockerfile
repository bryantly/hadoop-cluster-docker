FROM serf-dnsmasq

MAINTAINER KiwenLau <kiwenlau@gmail.com>

# install openssh-server, vim and openjdk
RUN apt-get install -y openssh-server vim

# move all configuration files into container
ADD files/* /tmp/
ADD http://download.oracle.com/otn-pub/java/jdk/8u65-b17/jre-8u65-linux-x64.tar.gz /opt/
ADD http://www.apache.org/dyn/closer.cgi/hadoop/common/hadoop-2.7.1/hadoop-2.7.1.tar.gz /opt/
ADD http://downloads.typesafe.com/scala/2.11.7/scala-2.11.7.tgz /opt/
ADD http://d3kbcqa49mib13.cloudfront.net/spark-1.6.0-bin-hadoop2.6.tgz /opt/

#configure ssh free key access
RUN mkdir /var/run/sshd && \
ssh-keygen -t rsa -f ~/.ssh/id_rsa -P '' && \
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
mv /tmp/ssh_config ~/.ssh/config && \
sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

#install packages
RUN ln -s /opt/jre1.8.0_66 /opt/java && \
ln -s /opt/scala-2.11.7 /opt/scala && \
ln -s /opt/hadoop-2.7.1 /opt/hadoop && \
ln -s /opt/spark-1.5.1-bin-hadoop2.6 /opt/spark && \
mv /tmp/bashrc ~/.bashrc && \
mv /tmp/hadoop-env.sh /opt/hadoop/etc/hadoop/hadoop-env.sh 
