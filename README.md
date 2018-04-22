# Customised, hardened Docker image for nginx

* Entire container runs as non-root user
* Logs to stdout and stderr instead of files
* Listens on port 8080 instead of privileged port 80
* Supports read-only root filesystem with `/tmp` as writable tmpfs
* Content served from `/srv` by default

## Example usage

### Dockerfile for static files
```Dockerfile
FROM wisvch/nginx
COPY . /srv/
```

### Dockerfile with multi-stage Node.js build
```Dockerfile
FROM node:carbon AS builder
WORKDIR /src
COPY . .
RUN yarn
RUN yarn build

FROM wisvch/nginx
COPY --from=builder /src/build/ /srv/
```

### Building and running

```bash
docker build -t nginx .
docker run --rm -it -p 127.0.0.1:8080:8080 --tmpfs /tmp --read-only nginx
```
then open http://127.0.0.1:8080 in your browser.