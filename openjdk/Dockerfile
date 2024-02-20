FROM eclipse-temurin:21.0.2_13-jre-alpine

ENV TZ=Asia/Shanghai

# set timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo '$TZ' > /etc/timezone

# add font
RUN apk add bash curl fontconfig && apk add --update ttf-dejavu && fc-cache --force
