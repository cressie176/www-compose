# www-compose
A [Docker Compose](https://docs.docker.com/compose/) project for deploying www.stephen-cresswell.net

## Running Locally

### Create the docker network
```bash
docker network create www
```

### Generate a self signed certificate

```bash
mkdir -p containers/nginx/etc/ngnix/ssl
openssl req \
    -x509 \
    -nodes \
    -newkey rsa:4096 \
    -keyout containers/nginx/etc/ngnix/ssl/stephen-cresswell.key \
    -out containers/nginx/etc/ngnix/ssl/stephen-cresswell.pem \
    -days 9000
```

### Configure .env
```
HEALTHCHECK_INTERVAL=1m
HEALTHCHECK_TIMEOUT=5s
HEALTHCHECK_RETRIES=3
CONTAINERS_DIR=./containers
REPO_USER=
REPO_PASSWORD=
NEW_RELIC_AGENT_ENABLED=
NEW_RELIC_LICENSE_KEY=
NEW_RELIC_LOGGING_ENABLED=false
```

### Configure DNS
```
sudo echo '127.0.0.1     local.stephen-cresswell.net' >> /etc/hosts
```

### Start
```bash
docker-compose up -d www-app-local
```

