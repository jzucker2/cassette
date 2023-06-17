# Docker

I want slimmer images so I'm using `nginx` as the base image in actual downstream deploy front-ends.

This needs to include the common `nginx` config files to avoid replication.

## Example Client Dockerfile

For a `Dockerfile` like in [hal](https://github.com/jzucker2/hal/pull/40)

```
# start of Dockerfile
ARG CASSETTE_VERSION=0.4.3
FROM ghcr.io/jzucker2/cassette:${CASSETTE_VERSION} AS cassette_base

# then continue file below
...
# rest of Dockerfile above
...

# Now build deploy image below ...

# https://levelup.gitconnected.com/easy-optimization-of-your-react-docker-image-down-to-22mb-9d9e3a06870
# Choose NGINX as our base Docker image
FROM nginx:alpine

COPY --from=cassette_base nginx /etc/nginx/conf.d

# Set working directory to nginx asset directory
WORKDIR /usr/share/nginx/html

# Remove default nginx static assets
RUN rm -rf *

# Copy static assets from builder stage
COPY --from=build_prod /app/build .

# Entry point when Docker container has started
ENTRYPOINT ["nginx", "-g", "daemon off;"]
```

## Dev Work

* https://github.com/jzucker2/hal/pull/40
* https://github.com/jzucker2/cassette/pull/26
