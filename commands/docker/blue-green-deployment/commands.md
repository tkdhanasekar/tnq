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
