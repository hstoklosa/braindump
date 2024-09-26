# Recreate Containers from Fresh Images

## Solution 1

This will automatically pull a fresh image from the repo. It also won't use the cached version that is prebuilt with any parameters you've been using before.

```
docker-compose build --no-cache
```

**_REF:_** _https://stackoverflow.com/a/42970204/13910414_

## Solution 2

If not using it for a CI then `docker-compose up --force-recreate` will do the job. Otherwise,

```
docker-compose rm -f (stop and remove the containers and volumes)
docker-compose pull
docker-compose up --build -d
# Run some tests
./tests
docker-compose stop -t 1
```

Could be another step if image/s are coming from Dockerfile(s). `docker-compose build --no-cache --pull`.

**_REF:_** _https://stackoverflow.com/a/32618288/13910414_
