# Redis Docker

Redis 8 (Alpine) with AOF persistence. Data persists in `./data`.

## Start

```bash
cp .env.example .env
# set REDIS_PASSWORD (openssl rand -hex 32)
mkdir -p data
docker compose up -d
```

## Verify

```bash
docker compose ps
docker compose logs -f redis
docker exec -it redis redis-cli -a YOUR_PASSWORD ping
```

Expected output:

```text
PONG
```

## Connection

```env
REDIS_URL=redis://:YOUR_PASSWORD@localhost:6379
```

## Common Commands

```redis
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

## Monitoring

### Logs

```bash
docker logs -f redis
```

### Memory Usage

```bash
docker exec -it redis redis-cli -a YOUR_PASSWORD INFO memory
```

### Connected Clients

```bash
docker exec -it redis redis-cli -a YOUR_PASSWORD CLIENT LIST
```

### Server Info

```bash
docker exec -it redis redis-cli -a YOUR_PASSWORD INFO
```

## Backup & Restore

### Backup

```bash
tar -czf redis-backup-$(date +%F).tar.gz data/
```

### Restore

> Stop Redis before restoring.

```bash
docker compose down

rm -rf data
tar -xzf redis-backup-YYYY-MM-DD.tar.gz

docker compose up -d
```

## License

[MIT](LICENSE)
