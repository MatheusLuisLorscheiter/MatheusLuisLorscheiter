# Local container health lab

Goal: observe the relationship between process status, application health and network connectivity using a disposable HTTP service.

Requirements: Docker Engine, Docker Compose v2 and curl.

```sh
docker compose up -d
docker compose ps
curl --fail http://127.0.0.1:8080/
docker compose logs --tail=30 web
docker compose down
```

The service is bound to loopback only. The health check tests the HTTP endpoint inside the container. The initial image download requires network access.

Exercises: stop the service and observe the request failure; restart it and check recovery; compare health status against the application response. Do not use production hosts for this lab.

This is an illustrative configuration; execution has not been independently validated here.
