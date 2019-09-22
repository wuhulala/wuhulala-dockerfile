FROM java:8

MAINTAINER wuhulala xueaohui_com@163.com
ENV REFRESHED_AT 2018-08-27

ENV zookeeper_addr=zookeeper:2181
COPY KafkaOffsetMonitor-assembly-0.4.6.jar /opt/
#

EXPOSE 8081

WORKDIR /opt/
#RUN tar -zxvf /opt/kafka_2.11-1.1.1.tgz -C /opt/kakfa
ENTRYPOINT java  -cp KafkaOffsetMonitor-assembly-0.4.6.jar com.quantifind.kafka.offsetapp.OffsetGetterWeb --offsetStorage kafka  --zk ${zookeeper_addr} --port 8081  --refresh 10.seconds  --retain 2.days --dbName offsetapp_kafka

