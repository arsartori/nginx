# nginx

### Atualizar nginx
    docker compose cp conf/default.conf nginx:/etc/nginx/conf.d/
### Atualizar node1
    docker compose exec node1 sed -i 's/$remote_addr/$http_x_real_ip/' /etc/nginx/nginx.conf
    docker compose exec node1 nginx -t
    docker compose exec node1 nginx -s reload

### Atualizar node2
    docker compose cp conf/index.html node2:/usr/share/nginx/html/
    docker compose exec node2 sed -i 's/$remote_addr/$http_x_real_ip/' /etc/nginx/nginx.conf