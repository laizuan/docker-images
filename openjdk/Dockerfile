FROM eclipse-temurin:21.0.5_11-jre-alpine

ENV TZ=Asia/Shanghai

RUN cat /etc/os-release

# set timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo '$TZ' > /etc/timezone

# add font
RUN apk add bash curl fontconfig && apk add --update ttf-dejavu && fc-cache --force


# 更新包管理器并安装依赖
RUN apk add --no-cache \
    bash \
    perl \
    perl-app-cpanminus \
    perl-dbd-mysql \
    perl-dbi \
    perl-yaml \
    mariadb-client \
    make \
    gcc \
    libc-dev \
    wget \
    curl \
    && cpanm --notest \
    JSON \
    Time::HiRes \
    DBI \
    DBD::mysql \
    && curl -LO https://downloads.percona.com/downloads/percona-toolkit/percona-toolkit-3.6.0/source/tarball/percona-toolkit-3.6.0.tar.gz \
    && tar -xzf percona-toolkit-LATEST.tar.gz \
    && cd percona-toolkit-* \
    && perl Makefile.PL \
    && make && make install \
    && cd .. \
    && rm -rf percona-toolkit-* percona-toolkit-LATEST.tar.gz \
    && apk del make gcc libc-dev

CMD ["pt-archiver", "--version"]
