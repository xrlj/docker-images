## rabbitmq

    docker run --hostname xrlj-rabbit --restart=always --name xrlj-rabbitmq -v /server/data/rabbitmq:/var/lib/rabbitmq  -e RABBITMQ_DEFAULT_USER=xrlj -e RABBITMQ_DEFAULT_PASS=123456 -e RABBITMQ_DEFAULT_VHOST=xrlj_vhost  -p 15672:15672 -p 4369:4369 -p 5671-5672:5671-5672 -p 15671:15671 -p 25672:25672 -d rabbitmq:3-management
    
## redis

    