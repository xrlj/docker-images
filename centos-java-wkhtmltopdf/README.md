## commit命令制作镜像 

    docker commit -a "xinxiamu" -m "centos7,java,wkhtmltopdf" 6924fb0a501b xinxiamu/wkhtmltopdf-java:v1
    
    -----上传镜像
    
    docker push xinxiamu/wkhtmltopdf-java:v1