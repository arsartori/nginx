# nginx

## 1) Servidor web HTTP (https://nginx.org/en/)

    docker pull nginx:latest
    docker run -d --name nginx -p 80:80 -p 443:443 nginx:latest

## 2) Proxy Reverso

    docker pull nginx:latest
    docker run -d --name nginx -p 80:80 -p 443:443 nginx:latest
    
## 3) Balanceador de carga

### Atualizar nginx
    docker compose cp conf/default.conf nginx:/etc/nginx/conf.d/
### Atualizar node1
    docker compose exec node1 sed -i 's/$remote_addr/$http_x_real_ip/' /etc/nginx/nginx.conf
    docker compose exec node1 nginx -t
    docker compose exec node1 nginx -s reload

### Atualizar node2
    docker compose cp conf/index.html node2:/usr/share/nginx/html/
    docker compose exec node2 sed -i 's/$remote_addr/$http_x_real_ip/' /etc/nginx/nginx.conf