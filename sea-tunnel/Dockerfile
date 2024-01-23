FROM openjdk:8

ENV SEATUNNEL_VERSION="2.3.3"
COPY /apache-seatunnel-${SEATUNNEL_VERSION}-bin.tar.gz /opt/apache-seatunnel-${SEATUNNEL_VERSION}-bin.tar.gz
WORKDIR /opt
RUN tar -xzvf apache-seatunnel-${SEATUNNEL_VERSION}-bin.tar.gz
RUN mv apache-seatunnel-${SEATUNNEL_VERSION} seatunnel
RUN rm -f /opt/apache-seatunnel-${SEATUNNEL_VERSION}-bin.tar.gz
WORKDIR /opt/seatunnel
ENTRYPOINT ["sh","-c"," bin/seatunnel.sh --config $config  -e local"]
