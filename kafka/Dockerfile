FROM java:8

MAINTAINER wuhulala xueaohui_com@163.com
ENV REFRESHED_AT 2018-08-27
# 环境配置
ENV broker_id=1
ENV zookeeper_addr=zookeeper:2181
ENV kafka_port=9092

# 自动解压
ADD kafka_2.11-1.1.1.tgz /opt/
RUN mv /opt/kafka_2.11-1.1.1 /opt/kafka

# 修改时区
ADD Shanghai /usr/share/zoneinfo/$TZ
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

#

VOLUME /opt/kafka/logs
VOLUME /opt/kafka/data

WORKDIR /opt/kafka/

ENTRYPOINT sed -i "65cnum.partitions=4" /opt/kafka/config/server.properties && sed -i "60clog.dirs=/opt/kafka/data" /opt/kafka/config/server.properties  && sed -i "31clisteners=PLAINTEXT://kafka${broker_id}:${kafka_port}" /opt/kafka/config/server.properties && sed -i "123czookeeper.connect=${zookeeper_addr}" /opt/kafka/config/server.properties && sed -i "21cbroker.id=${broker_id}" /opt/kafka/config/server.properties  && /opt/kafka/bin/kafka-server-start.sh /opt/kafka/config/server.properties

