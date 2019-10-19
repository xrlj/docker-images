## 执行Dockerfile制作镜像 

    docker build -t xinxiamu/wkhtmltopdf-java:latest .
    
## 上传镜像到公共仓库
    
    [root@xr-server-dev centos-java-wkhtmltopdf]# docker login
    Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
    Username (xinxiamu): xinxiamu
    Password: 
    Login Succeeded
    [root@xr-server-dev centos-java-wkhtmltopdf]# docker push xinxiamu/wkhtmltopdf-java:latest 
    The push refers to repository [docker.io/xinxiamu/wkhtmltopdf-java]
    6aa513e2e805: Pushed 
    9c738a174b81: Pushed 
    a3b033142ac0: Pushed 
    e132658139f6: Pushed 
    865f8a72076b: Pushed 
    d69483a6face: Layer already exists 
    latest: digest: sha256:7230d89f00122d47ffbb020ae2cb51283c87e24a2bc85f73ecb82c9b92b26725 size: 1588