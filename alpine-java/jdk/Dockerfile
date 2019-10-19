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

ARG VER_JAVA_MAJOR=11.0.5
ARG VER_JAVA_MINOR=10
ARG DIR_JAVA_BASE=/usr/local/share/java
ARG DIR_JAVA_HOME=${DIR_JAVA_BASE}/jdk-${VER_JAVA_MAJOR}
ARG ARC_MODE=x64
ARG JDK_DOWNLOAD_URL=https://download.oracle.com/otn/java/jdk/${VER_JAVA_MAJOR}+${VER_JAVA_MINOR}/e51269e04165492b90fa15af5b4eb1a5/jdk-${VER_JAVA_MAJOR}_linux-${ARC_MODE}_bin.tar.gz?AuthParam=1571451821_7fe5fbb8ccfff70d94c31a87a7b59f9f
ARG VER_GLIBC=2.29-r0
ARG GLIBC_DOWNLOAD_URL=https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${VER_GLIBC}
 
RUN mkdir -p ${DIR_JAVA_HOME} && \
    wget --header "Cookie: oraclelicense=accept-securebackup-cookie" ${JDK_DOWNLOAD_URL} &&\
    tar zxf jdk-${VER_JAVA_MAJOR}_linux-${ARC_MODE}_bin.tar.gz -C ${DIR_JAVA_BASE} && \
    apk upgrade --update-cache &&\
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub &&\
    wget ${GLIBC_DOWNLOAD_URL}/glibc-${VER_GLIBC}.apk &&\
    wget ${GLIBC_DOWNLOAD_URL}/glibc-bin-${VER_GLIBC}.apk &&\
    wget ${GLIBC_DOWNLOAD_URL}/glibc-i18n-${VER_GLIBC}.apk &&\
    apk  add glibc-${VER_GLIBC}.apk glibc-bin-${VER_GLIBC}.apk glibc-i18n-${VER_GLIBC}.apk &&\
    sleep 2 &&\
    rm -rf /tmp/* /var/cache/apk/* jdk-${VER_JAVA_MAJOR}_linux-${ARC_MODE}_bin.tar.gz &&\
    /usr/glibc-compat/bin/localedef -i en_US -f UTF-8 en_US.UTF-8
 
ENV JAVA_HOME ${DIR_JAVA_HOME}
ENV PATH      $PATH:${DIR_JAVA_HOME}/bin
ENV LANG      en_US.UTF8