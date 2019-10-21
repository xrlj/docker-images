###############################################################################
#
#IMAGE:   Oracle-JDK-Image
#VERSION: Alpine: 3.9
#VERSION: JDK   :Oracle 11.0.5
#
###############################################################################
FROM alpine:3.9

###############################################################################
#MAINTAINER
###############################################################################
MAINTAINER xinxiamu <932852117@qq.com>

#更新Alpine的软件源为国内（清华大学）的站点，因为从默认官源拉取实在太慢了。。。
#RUN echo "https://mirror.tuna.tsinghua.edu.cn/alpine/v3.9/main/" > /etc/apk/repositories
## 阿里
RUN echo "http://mirrors.aliyun.com/alpine/latest-stable/main/" > /etc/apk/repositories

##因为COPY命令会新建一层镜像，所以会使得最终镜像非常大。
##改用网络下载方式，把jdk放到自己的文件服务器
#COPY doc/jdk-11.0.5_linux-x64_bin.tar.gz /tmp

ARG JAVA_DOWLOAD_URL=http://39.108.191.220/jdk-11.0.5_linux-x64_bin.tar.gz
ARG GLIBC_VERSION=2.30-r0
ARG GLIBC_DOWNLOAD_URL=https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}
ARG JAVA_VERSION=11.0.5
ARG ARC_MODE=x64
ARG DIR_JAVA_HOME=/opt/java

RUN set -ex && \
    apk -U upgrade --update-cache && \
    apk add --no-cache libstdc++ ca-certificates bash bash-doc bash-completion && \
    cd /tmp && \
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    wget ${GLIBC_DOWNLOAD_URL}/glibc-${GLIBC_VERSION}.apk && \
    wget ${GLIBC_DOWNLOAD_URL}/glibc-bin-${GLIBC_VERSION}.apk && \
    wget ${GLIBC_DOWNLOAD_URL}/glibc-i18n-${GLIBC_VERSION}.apk && \
    apk add /tmp/*.apk && \
    ( /usr/glibc-compat/bin/localedef --force --inputfile POSIX --charmap UTF-8 C.UTF-8 || true ) && \
    echo "export LANG=C.UTF-8" > /etc/profile.d/locale.sh && \
    /usr/glibc-compat/sbin/ldconfig /lib /usr/glibc-compat/lib && \
    wget "https://www.archlinux.org/packages/core/x86_64/zlib/download" -O /tmp/libz.tar.xz && \
    mkdir -p /tmp/libz && \
    tar -xf /tmp/libz.tar.xz -C /tmp/libz && \
    cp /tmp/libz/usr/lib/libz.so.1.2.11 /usr/glibc-compat/lib && \
    /usr/glibc-compat/sbin/ldconfig && \
    wget ${JAVA_DOWLOAD_URL} && \
    mkdir -p ${DIR_JAVA_HOME} && \
    tar zxf jdk-${JAVA_VERSION}_linux-${ARC_MODE}_bin.tar.gz -C ${DIR_JAVA_HOME} && \
    sleep 2 && \
    rm -rf /tmp/* /var/cache/apk/*

ENV JAVA_HOME ${DIR_JAVA_HOME}/jdk-${JAVA_VERSION}
ENV PATH      $PATH:${DIR_JAVA_HOME}/jdk-${JAVA_VERSION}/bin
ENV LANG      C.UTF-8