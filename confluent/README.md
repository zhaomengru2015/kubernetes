# Confluent Demo

## Development

```shell
docker-compose up -d
docker-compose restart control-center
```

## Cleanup

```shell
docker-compose stop
docker system prune -a --volumes --filter "label=io.confluent.docker"
```
