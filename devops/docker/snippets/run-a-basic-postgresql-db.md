# Run A Basic PostgreSQL Database

A basic PostgreSQL database that runs on port `8080` and lives in a docker container that is created through the `docker-compose.yml` file.

```yaml
version: "3"
services:
  postgres:
    image: postgres:latest
    restart: always
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=database_name
    ports:
      - "8080:8080"
    volumes:
      - data-volume:/data/db

volumes:
  data-volume:
```

This command knows to look for the docker-compose.yml file though you can always be explicit about the file with the `-f` argument.

This configuration uses the latest image of PostgreSQL, however you can change it by setting the image to something like `postgres:15` or `postgres:alpine`.
