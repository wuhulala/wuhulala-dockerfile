FROM base

MAINTAINER wuhulala xueaohui_com@163.com
ENV REFRESHED_AT 2018-08-27


# 自动解压
ADD jdk-8u181-linux-x64.tar.gz /opt/
RUN mkdir -p /usr/java/
RUN mv /opt/jdk1.8.0_181 /usr/java/

# 修改时区
ENV JAVA_HOME=/usr/java/jdk1.8.0_181
ENV PATH=$PATH:$JAVA_HOME/bin
ENV CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar