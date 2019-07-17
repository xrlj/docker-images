FROM centos

RUN yum -y update \
&& yum clean all \
&& yum install wget \
&& cd /tmp \
&& wget java-url \

ENTRYPOINT ["/bin/bash"]
