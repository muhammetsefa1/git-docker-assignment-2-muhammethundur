# Git and Docker Starter Application

This repository contains a small Python web application used to practice Git, GitHub, and Docker workflows.

## Application

The application listens on port 8000 and returns a text response when accessed over HTTP.

## Verification

The running application should be verified using an HTTP request to port 8000.

## Build and run

```sh
docker build -t git-docker-app:test .
docker run -d --name app-test -p 8080:8000 git-docker-app:test
curl http://localhost:8080
docker logs app-test
docker rm -f app-test
```

The host uses port 8080; the container listens on port 8000. The response
includes the NetID health status, version, and course. The image creates
`/app/logs` during the build.

## Verify container networking

```sh
docker network create app-net
docker run -d --name app-test --network app-net git-docker-app:test
docker run --rm --name network-test --network app-net curlimages/curl:8.5.0 http://app-test:8000
docker rm -f app-test
docker network rm app-net
```

On `app-net`, Docker resolves the application by its container name.
