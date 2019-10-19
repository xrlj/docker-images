## 执行Dockerfile制作镜像 

    docker build -t xinxiamu/jre-server:11 .
    
## 下载glibc

由于网络的原因，所以不再Dockerfile中命令下载，先先下载好。

https://github.com/sgerrand/alpine-pkg-glibc/releases/    

## 测试

    docker run -it --rm xinxiamu/jre-server:11
    
    java -version

## 参考网址

1.https://github.com/anapsix/docker-alpine-java

2.https://blog.csdn.net/qq_36335313/article/details/92428635

