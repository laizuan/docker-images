FROM openjdk:8

COPY /seatunnel /opt/seatunnel
WORKDIR /opt/seatunnel
ENTRYPOINT ["sh","-c"," bin/seatunnel.sh --config $config  -e local"]
