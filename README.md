# Customised, hardened Docker image for nginx

* Entire container runs as non-root user
* Logs to stdout and stderr instead of files
* Listens on port 8080 instead of privileged port 80
* Supports read-only root filesystem with `/tmp` as writable tmpfs
* Content served from `/srv` by default
