http {
    # Зона для ограничения запросов: по IP клиента, размер 10 мегабайт, скорость 10 запросов в минуту
    limit_req_zone $binary_remote_addr zone=myzone:10m rate=10r/m;

    upstream backend_servers {
        server backend1.example.com;
        server backend2.example.com;
        server backend3.example.com;
    }

    server {
        listen 80;

        location / {
            # Применяем ограничение из зоны myzone
            limit_req zone=myzone;
            # Возвращаем HTTP 429 при превышении лимита
            limit_req_status 429;

            proxy_pass http://backend_servers;
        }
    }
}