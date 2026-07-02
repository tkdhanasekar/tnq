## To divert traffic to green deployment
```
cp nginx/green.conf nginx/active.conf
```
```
docker exec nginx nginx -s reload
```
## To divert traffic to blue deployment
```
cp nginx/blue.conf nginx/active.conf
```
```
docker exec nginx nginx -s reload
```

```
docker compose up -d --build

curl http://localhost

Deploy New Version
docker compose build green
docker compose up -d green
docker inspect green \
  --format='{{json .State.Health.Status}}'
```
