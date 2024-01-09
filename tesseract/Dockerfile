FROM debian:12

RUN apt-get update && apt-get install --no-install-recommends --yes \
    apt-transport-https \
    asciidoc \
    automake \
    bash \
    ca-certificates \
    curl \
    docbook-xsl \
    g++ \
    git \
    libleptonica-dev \
    libtool \
    libicu-dev \
    libpango1.0-dev \
    libcairo2-dev \
    make \
    pkg-config \
    wget \
    xsltproc \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*


ENV OCR_VERSION="5.3.3" \
    TZ=Asia/Shanghai

# 设置时区
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo '$TZ' > /etc/timezone

WORKDIR /src

# 下载 tesseract ocr 解压并安装
RUN wget -qO tesseract.tar.gz https://codeload.github.com/tesseract-ocr/tesseract/tar.gz/refs/tags/$OCR_VERSION && \
    tar -xzf tesseract.tar.gz && \
    rm tesseract.tar.gz && \
    mv tesseract-* tesseract

WORKDIR /src/tesseract

RUN ./autogen.sh && \
    ./configure && \
    make && \
    make install && \
    ldconfig

# go to default traineddata directory
WORKDIR /usr/local/share/tessdata/
# copy language script and list to image
COPY get-languages.sh .
COPY languages.txt .

# make script executable
RUN chmod +x ./get-languages.sh
# download traineddata languages
RUN ./get-languages.sh

# 下载并编译训练库 tesstrain
# RUN git clone https://github.com/tesseract-ocr/tesstrain.git && \
#  cd ./tesstrain && \
#  pip install -r requirements.txt && make tesseract-langdata

# 设置环境变量
ENV JAVA_HOME /opt/java/openjdk
ENV TESSERACT_HOME /usr/local/tesseract
ENV TESSDATA_PREFIX=$TESSERACT_HOME/share/tessdata
ENV PATH $TESSERACT_HOME/bin:$TESSDATA_PREFIX:$JAVA_HOME/bin:$PATH

# 安装openjdk
WORKDIR /opt
RUN wget -qO java.tar.gz https://download.java.net/java/GA/jdk21.0.1/415e3f918a1f4062a0074a2794853d0d/12/GPL/openjdk-21.0.1_linux-x64_bin.tar.gz && \
 tar -xvf java.tar.gz && \
 rm java.tar.gz && \
 cd ./java && \
 mv jdk-* openjdk


RUN set -eux; \
    echo "Verifying install ..."; \
    echo "java --version"; java --version; \
    echo "Jdk install complete."

WORKDIR /tmp/

# Test tesseract ocr
CMD ["tesseract", "--list-langs"]
