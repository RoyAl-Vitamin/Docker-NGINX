# Docker-NGINX
Пример работы балансера, встроенного в  NGINX, с докером

## Запуск примера

Для нашего HTTP сервера мы будем использовать [HAProxy](https://www.haproxy.com/), создадим контейнер с HAProxy, которые будет слушать порт 80 и заниматься балансировкой запросов к различным Node.js контейнерам на порту 8080 `index.js`. Что бы создать наши контейнеры (Node.js apps and HAProxy - `Dockerfile`), воспользуемся Docker Compose `docker-compose.yml`. Мы так же определим переменную окружения `BALANCE` что бы настроить алгоритм балансировки leastconn вместо roundrobin, который работает по умолчанию.

Соберём докер образ с помощью команды

```terminal
docker build -t awesome .
```

Инициализировать и запустить Docker Swarm:

```terminal
docker swarm init
docker stack deploy --compose-file=docker-compose.yml prod
```

Пример взят с [сайта](https://medium.com/@nirgn/load-balancing-applications-with-haproxy-and-docker-d719b7c5b231).
