```jsx
http {
    # Настройка upstream для балансировки нагрузки
    upstream backend_servers {
        server backend1.example.com;
        server backend2.example.com;
        server backend3.example.com;
    }

    # Зона для ограничения запросов
    limit_req_zone $binary_remote_addr zone=rate_limit_zone:10m rate=10r/m;

    server {
        listen 80;

        # Ограничение запросов на все маршруты
        location / {
            limit_req zone=rate_limit_zone;
            limit_req_status 429;

            proxy_pass http://backend_servers;
        }
    }
}
```