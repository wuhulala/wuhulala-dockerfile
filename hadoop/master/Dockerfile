FROM centos:7.6.1810

MAINTAINER wuhulala@qq.com

WORKDIR /root


# install jdk
ADD common/res/jdk-8u212-linux-x64.tar.gz /usr/java/

# install hadoop
ADD common/res/hadoop-2.7.7.tar.gz /usr/local/hadoop

# install openssh-server
RUN yum -y install openssh-server openssh-clients

# set environment variable
ENV JAVA_HOME=/usr/java/jdk1.8.0_212
ENV HADOOP_HOME=/usr/local/hadoop/hadoop-2.7.7/
ENV PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:/usr/java/jdk1.8.0_212/bin

# ssh without key
RUN ssh-keygen -t rsa -f ~/.ssh/id_rsa -P '' && \
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys


# create base bir
RUN mkdir -p ~/hdfs/namenode && \ 
    mkdir -p ~/hdfs/datanode && \
    mkdir $HADOOP_HOME/logs

# copy config
COPY common/config/* /tmp/

RUN mv /tmp/ssh_config ~/.ssh/config && \
    mv /tmp/hadoop-env.sh $HADOOP_HOME/etc/hadoop/hadoop-env.sh && \
    mv /tmp/hdfs-site.xml $HADOOP_HOME/etc/hadoop/hdfs-site.xml && \ 
    mv /tmp/core-site.xml $HADOOP_HOME/etc/hadoop/core-site.xml && \
    mv /tmp/mapred-site.xml $HADOOP_HOME/etc/hadoop/mapred-site.xml && \
    mv /tmp/yarn-site.xml $HADOOP_HOME/etc/hadoop/yarn-site.xml && \
    mv /tmp/slaves $HADOOP_HOME/etc/hadoop/slaves && \
    mv /tmp/start-hadoop.sh ~/start-hadoop.sh && \
    mv /tmp/start-master.sh ~/start-master.sh && \
    mv /tmp/run-wordcount.sh ~/run-wordcount.sh

# start dfs yarn
RUN chmod +x ~/start-hadoop.sh && \
    chmod +x ~/run-wordcount.sh && \
    chmod +x $HADOOP_HOME/sbin/start-dfs.sh && \
    chmod +x $HADOOP_HOME/sbin/start-yarn.sh 

WORKDIR $HADOOP_HOME/bin

RUN yum -y install which

# format namenode
RUN $HADOOP_HOME/bin/hdfs namenode -format hadoop-cluster

# 修改时区
ADD common/res/Shanghai /usr/share/zoneinfo/$TZ
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# 
RUN sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key
RUN ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key

CMD [ "sh", "-c", "/usr/sbin/sshd -D"]