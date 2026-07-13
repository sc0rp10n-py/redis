Start

```
mkdir data
docker compose up -d
```

Verify
```
docker compose ps
docker compose logs -f redis
docker exec -it redis redis-cli -a YOUR_PASSWORD ping
```

Connect URL
```
REDIS_URL=redis://:YOUR_PASSWORD@localhost:6379
```

Common Redis operations
```
SET key value
GET key
DEL key

EXISTS key

EXPIRE key 3600

TTL key

INCR counter

LPUSH queue job1

RPOP queue

HSET user:1 name John

HGETALL user:1
```

Monitoring

View logs:
```
docker logs -f redis
```
View memory usage:
```
docker exec -it redis redis-cli -a YOUR_PASSWORD INFO memory
```
View connected clients:
```
docker exec -it redis redis-cli -a YOUR_PASSWORD CLIENT LIST
```
View overall server info:
```
docker exec -it redis redis-cli -a YOUR_PASSWORD INFO
```