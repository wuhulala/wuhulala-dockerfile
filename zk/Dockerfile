FROM java:8
MAINTAINER wuhulala xueaohui_com@163.com
ENV REFRESHED_AT 2018-08-27

ADD zookeeper-3.4.10.tar.gz /opt/

WORKDIR /opt/zookeeper-3.4.10

EXPOSE 2181

ENTRYPOINT /opt/zookeeper-3.4.10/bin/zkServer.sh start-foreground

