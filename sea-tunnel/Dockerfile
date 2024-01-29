FROM openjdk:8

COPY /apache-seatunnel-bin.tar.gz /opt/apache-seatunnel-bin.tar.gz
WORKDIR /opt
RUN tar -xzvf apache-seatunnel-bin.tar.gz
RUN mv apache-seatunnel seatunnel
RUN rm -f /opt/apache-seatunnel-bin.tar.gz
WORKDIR /opt/seatunnel
ENTRYPOINT ["sh","-c"," bin/seatunnel.sh --config $config  -e local"]
