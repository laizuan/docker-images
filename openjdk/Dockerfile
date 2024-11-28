FROM eclipse-temurin:21.0.5_11-jre-alpine

ENV TZ=Asia/Shanghai

RUN cat /etc/os-release

# set timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo '$TZ' > /etc/timezone

# add font
RUN apk add bash curl fontconfig && apk add --update ttf-dejavu && fc-cache --force

RUN apk add percona-toolkit

CMD ["pt-archiver", "--version"]
