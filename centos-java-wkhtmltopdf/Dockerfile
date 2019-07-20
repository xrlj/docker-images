FROM centos

COPY doc/jre-8u221-linux-x64.rpm /tmp
COPY doc/wkhtmltox-0.12.5-1.centos7.x86_64.rpm /tmp

##解决中文乱码，安装中文包
RUN yum install kde-l10n-Chinese -y \
&& yum install glibc-common -y \
&& localedef -c -f UTF-8 -i zh_CN zh_CN.utf8 \
&& export LANG=zh_CN.UTF-8 \
&& echo "export LANG=zh_CN.UTF-8" >> /etc/locale.conf \
##解决中文乱码，安装中文包 end
&& yum install  zlib fontconfig freetype libX11 libXext libXrender libjpeg libpng openssl xorg-x11-fonts-75dpi xorg-x11-fonts-Type1 -y \
&& cd /tmp \
&& rpm -i jre-8u221-linux-x64.rpm \
&& rpm -i wkhtmltox-0.12.5-1.centos7.x86_64.rpm \
&& rm -rf * \
&& yum clean all

## wkhtmtopdf字体包，解决中文乱码，添加其它字体包
COPY doc/simsun.ttc /usr/share/fonts
COPY doc/arial/*.ttf /usr/share/fonts/

##指定系统语言环境
ENV LANG zh_CN.UTF-8
ENV LC_ALL zh_CN.UTF-8

ENTRYPOINT ["/bin/bash"]
