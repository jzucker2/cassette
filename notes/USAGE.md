# Usage

This is not intended to be its own project but 
to be used as a base image for many react projects.

## Example `Dockerfile`

Note we are not running `yarn install` here 
but we are still running `yarn build`.

```Dockerfile
ARG CASSETTE_VERSION=0.3.0
FROM ghcr.io/jzucker2/cassette:${CASSETTE_VERSION} AS linux_base

FROM linux_base AS node_dependencies

WORKDIR /app

# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

COPY package.json package.json

COPY yarn.lock yarn.lock

FROM node_dependencies AS source_code
COPY public/ public/

COPY src/ src/

FROM source_code AS build_prod
RUN yarn build

# this needs to match the env var in the app
EXPOSE 3000

FROM build_prod AS run_server
CMD ["serve", "-s", "build", "-l", "3000"]
```

## Base Image

This is a base image for react projects. 
For more info on node (+ react) base images, see [tapedeck](https://github.com/jzucker2/tapedeck)
