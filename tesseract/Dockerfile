FROM ubuntu:22.04

RUN apt update && apt install -y git autoconf automake libtool pkg-config libpng-dev libjpeg8-dev libtiff5-dev zlib1g-dev libwebpdemux2 libwebp-dev libopenjp2-7-dev libgif-dev libarchive-dev libcurl4-openssl-dev libicu-dev libpango1.0-dev libcairo2-dev libleptonica-dev wget python3-pip

ENV OCR_VERSION="5.3.3" \
    BASE_WORKDIR="/home/leaderrun" \
    JAVA_OPTS="" \
    PORT="5432" \
    TESSDATA_PREFIX="/usr/local/share/tessdata" \
    TZ=Asia/Shanghai

# 设置时区
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo '$TZ' > /etc/timezone

# 下载 tesseract ocr 解压并安装
RUN wget -O tesseract.tar.gz -p https://codeload.github.com/tesseract-ocr/tesseract/tar.gz/refs/tags/$OCR_VERSION
RUN tar -zxvf tesseract.tar.gz
RUN cd ./tesseract-$OCR_VERSION && \
    ./autogen.sh && \
    ./configure && \
    make && make install && \
    make training && make training-install

# 下载并编译训练库 tesstrain
RUN git clone https://github.com/tesseract-ocr/tesstrain.git && \
 cd ./tesstrain && \
 pip install -r requirements.txt && make tesseract-langdata

# Test tesseract ocr


# 安装openjdk
RUN wget -O openjdk-21.tar.gz -p https://download.java.net/java/GA/jdk21.0.1/415e3f918a1f4062a0074a2794853d0d/12/GPL/openjdk-21.0.1_linux-x64_bin.tar.gz
RUN tar -zxvf openjdk-21.tar.gz
ENV JAVA_HOME /jdk-21.0.1
ENV PATH $PATH:$JAVA_HOME/bin

## 删除压缩包
RUN rm -rf tesseract.tar.gz openjdk-21.tar.gz

CMD ["tesseract", "--list-langs"]
