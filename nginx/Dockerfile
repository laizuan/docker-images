# node 构建
FROM node:18-alpine as build-stage

WORKDIR /app
COPY . ./
# 设置 node 阿里镜像
RUN npm config set registry https://registry.npmmirror.com/
# 设置--max-old-space-size
ENV NODE_OPTIONS=--max-old-space-size=16384

RUN npm install pnpm -g && \
    pnpm install --frozen-lockfile && \
    pnpm build:docker

RUN echo "🎉 打包成功 🎉"

FROM nginx:stable-alpine as production-stage

ENV TZ=Asia/Shanghai

# set timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo '$TZ' > /etc/timezone

COPY --from=build-stage /app/dist /usr/share/nginx/html
COPY ./nginx.conf /etc/nginx/nginx.conf
