FROM nginx:stable-alpine

ENV TZ=Asia/Shanghai

# set timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo '$TZ' > /etc/timezone

RUN echo "types { application/javascript js mjs; }" > /etc/nginx/conf.d/mjs.conf

COPY ./nginx.conf /etc/nginx/nginx.conf
