#
# Hive MQ Dockerfile
#
FROM java:8

ENV HIVEMQZIPFILE hivemq-3.1.5.zip
ENV MQTTMESSAGELOGZIPFILE mqtt-message-log-3.0.0.zip

COPY hivemq-* /tmp/
COPY mqtt-message-log-* /tmp/

RUN \
    cd /tmp && \
    unzip $HIVEMQZIPFILE -d /opt/ &&\
    rm -f $HIVEMQZIPFILE &&\
    mv /opt/hivemq-* /opt/hivemq &&\
    unzip $MQTTMESSAGELOGZIPFILE -d /opt/ &&\
    rm -f $MQTTMESSAGELOGZIPFILE &&\
    mv /opt/mqtt-message-log-* /opt/hivemq/plugins/ &&\
	sed -i -- 's/#JAVA_OPTS=\"$JAVA_OPTS -DdiagnosticMode=true\"/#JAVA_OPTS=\"$JAVA_OPTS -DdiagnosticMode=true\"/g' /opt/hivemq/bin/run.sh


# Install the HiveMQ config file
COPY config.xml /opt/hivemq/conf/config.xml
  
RUN useradd -c 'HiveMQ user' -m -d /home/hivemq -s /bin/bash hivemq
RUN chown -R hivemq.hivemq /opt/hivemq
USER hivemq
ENV HOME /home/hivemq

# Define HIVEMQ_HOME variable
ENV HIVEMQ_HOME /opt/hivemq

# Expose MQTT port
EXPOSE 1883
# Expose MQTT over Websocket port
EXPOSE 8000
# Expose Cluster ports for UDP and TCP failure connection
EXPOSE 7800
EXPOSE 7900

CMD ["/opt/hivemq/bin/run.sh"]
