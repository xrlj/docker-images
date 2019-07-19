FROM centos

##解决中文乱码
RUN  yum -y update \
&& yum clean all \
&& yum install kde-l10n-Chinese -y \
&& yum install glibc-common -y \
&& localedef -c -f UTF-8 -i zh_CN zh_CN.utf8 \
&& export LANG=zh_CN.UTF-8 \
&& echo "export LANG=zh_CN.UTF-8" >> /etc/locale.conf \

ENV LANG zh_CN.UTF-8
ENV LC_ALL zh_CN.UTF-8

ENTRYPOINT ["/bin/bash"]
