FROM openjdk:8

ENV SEATUNNEL_VERSION="2.3.3"
COPY /seatunnel /opt/seatunnel
WORKDIR /opt/seatunnel
ENTRYPOINT ["sh","-c"," bin/seatunnel.sh --config $config  -e local"]
