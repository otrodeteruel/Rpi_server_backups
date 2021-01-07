# Minimal web server nginx

Servidor html minimo

docker run -d --name=d_nginx -v ./index/public:/usr/share/nginx/html:ro -p 80:80 nginx:alpine


## docker-compose

  index:
    image: nginx:alpine
    restart: always
    container_name: nginx_index
    ports:
      - 80:80
    volumes:
      - ./index/public:/usr/share/nginx/html:ro
