FROM alpine:3.9
MAINTAINER mvpbang mvpbang@qq.com
###alpine+bash

COPY .bashrc /root/
RUN set -x \
    apk update \
    && apk add --no-cache bash bash-doc bash-completion \
    && sed -i 's/ash/bash/g' /etc/passwd \
    && source /root/.bashrc
CMD ["/bin/bash"]