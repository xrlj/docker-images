# centos 7
FROM centos:latest

# run
RUN yum install wget -y \
  &&    mkdir /shadowsocks \
  &&    cd /shadowsocks  \
  &&    wget https://xinxiamu.github.io/2017/11/11/shadowsocks-go/server.tar.gz    \
  &&    tar -zxvf server.tar.gz    \
  &&    cd /server  \
  &&    chmod a+x shadowsocks-server    \
  &&    chmod +x shadowsocks.sh

# export config
VOLUME /shadowsocks

EXPOSE 8388 1080
ENTRYPOINT ["/shadowsocks/server/shadowsocks.sh"]
