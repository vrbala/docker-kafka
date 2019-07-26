# Kafka and Zookeeper

FROM openjdk:8-alpine

ENV SCALA_VERSION 2.11
ENV KAFKA_VERSION 2.2.0
ENV KAFKA_HOME /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"

# Install bash
RUN /bin/sh -c "apk add --no-cache bash"

# Install supervisor
RUN /bin/sh -c "apk add --no-cache supervisor"

# Install Kafka
RUN wget -q http://apache.mirrors.spacedump.net/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -O /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz && \
    tar xfz /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -C /opt && \
    rm /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz

RUN mkdir /etc/supervisor.d
ADD supervisor/kafka.ini /etc/supervisor.d/kafka.ini
ADD scripts/start-kafka.sh /usr/bin/start-kafka.sh

# 2181 is zookeeper, 9092 is kafka
EXPOSE 2181 9092

CMD ["supervisord", "-n"]
