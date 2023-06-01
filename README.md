# Kodbox deploy

## About Kodbox

[Kodbox](https://github.com/kalcaddle/kodbox)


# Deploy Kodbox

## Deploy Kodbox with docker-compose

### Modify data path in docker-compose.yaml

```yaml
version: '3.0'
services:
  kodcloud:
    container_name: kodcloud
    image: kodcloud/kodbox
    restart: always
    ports:
      - 10240:80
    depends_on:
      - mysql
      - redis

  mysql:
    container_name: mysql
    image: mysql:8.0.29
    restart: always
    volumes:
      - /Users/tsmax/docker/mysql/data:/var/lib/mysql
      - /Users/tsmax/docker/mysql/conf:/etc/mysql/conf.d
      - /Users/tsmax/docker/mysql/logs:/logs
    ports:
      - 9004:3306
    environment:
      - "MYSQL_ROOT_PASSWORD=2002"

  redis:
    container_name: redis
    image: redis:5.0
    restart: always
    volumes:
      - /Users/tsmax/docker/redis/data:/data
      - /Users/tsmax/docker/redis/redis.conf:/etc/redis/redis.conf
    ports:
      - 9005:6379
```

```shell
# Build image
docker-compose -f docker-compose.yaml up -d
```
