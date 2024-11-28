FROM eclipse-temurin:21.0.5_11-jre-alpine

ENV TZ=Asia/Shanghai

RUN cat /etc/os-release

# set timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo '$TZ' > /etc/timezone

# add font
RUN apk add bash curl fontconfig && apk add --update ttf-dejavu && fc-cache --force

RUN apt-get update && apt-get install -y \
    wget \
    gnupg \
    lsb-release \
    && wget https://repo.percona.com/apt/percona-release_latest.generic_all.deb \
    && dpkg -i percona-release_latest.generic_all.deb \
    && percona-release enable-only tools \
    && apt-get update && apt-get install -y \
    percona-toolkit \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

CMD ["pt-archiver", "--version"]
