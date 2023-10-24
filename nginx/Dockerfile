FROM nginx:stable-alpine

ENV TZ=Asia/Shanghai

# set timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo '$TZ' > /etc/timezone

COPY ./nginx.conf /etc/nginx/nginx.conf
