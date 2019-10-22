## 执行Dockerfile制作镜像 

    docker build -t xinxiamu/jre-server:11 .
    
## 下载glibc

由于网络的原因，所以不再Dockerfile中命令下载，先先下载好。

https://github.com/sgerrand/alpine-pkg-glibc/releases/    

## 测试

    docker run -it --rm xinxiamu/jre-server:11 java -version
    
这里测试的时候，会报错，显示java运行环境出错误。

1.错误描述：

    #
    # A fatal error has been detected by the Java Runtime Environment:
    #
    #  SIGSEGV (0xb) at pc=0x00007fab8b0e1ab1, pid=54, tid=69
    #
    # JRE version: Java(TM) SE Runtime Environment (13.0.1+9) (build 13.0.1+9)
    # Java VM: Java HotSpot(TM) 64-Bit Server VM (13.0.1+9, mixed mode, sharing, tiered, compressed oops, g1 gc, linux-amd64)
    # Problematic frame:
    # C  [libc.so.6+0x11dab1]
    #
    # Core dump will be written. Default location: /tmp/jdk-13.0.1/bin/core.54
    #
    # If you would like to submit a bug report, please visit:
    #   http://bugreport.java.com/bugreport/crash.jsp
    #
    
2.问题原因：

是因为缺少libz包相关东西。解决办法是到arch linux中下载相关包并安装修复。   

3.修复：

    wget "https://www.archlinux.org/packages/core/x86_64/zlib/download" -O /tmp/libz.tar.xz \
        && mkdir -p /tmp/libz \
        && tar -xf /tmp/libz.tar.xz -C /tmp/libz \
        && cp /tmp/libz/usr/lib/libz.so.1.2.11 /usr/glibc-compat/lib \
        && /usr/glibc-compat/sbin/ldconfig \
        && rm -rf /tmp/libz /tmp/libz.tar.xz  
        
再次测试，问题完美解决：

    /tmp/alpine-tools/jdk-11.0.5 # bin/java -version
    java version "11.0.5" 2019-10-15 LTS
    Java(TM) SE Runtime Environment 18.9 (build 11.0.5+10-LTS)
    Java HotSpot(TM) 64-Bit Server VM 18.9 (build 11.0.5+10-LTS, mixed mode)  
    
## java11生成jre模块

    jdk-${JAVA_VERSION}/bin/jlink --module-path jmods --add-modules java.desktop --output jre 

_注：_这样生成的jre无法运行spring-boot项目。应该是缺少模块。暂时没找到更好生成服务器的jre方法。

### 解决办法（建立jvm最小运行时环境）


    
## 过程记录

1.在Dockerfile中，使用COPY命令添加到镜像中，文件越大，制作出来的镜像越大，尽管最后都`rm -rf`掉,还是很大。所以，glibc-*.apk文件都改为直接从网络上拉取。

2.jdk11无法直接通过网络下载，所以只能先下载好，但是jdk很大，所以先通过命令生成jre文件，再COPY进去。               

## 参考网址

1.https://github.com/anapsix/docker-alpine-java

2.https://blog.csdn.net/qq_36335313/article/details/92428635

3.https://github.com/sgerrand/alpine-pkg-glibc/issues/75

