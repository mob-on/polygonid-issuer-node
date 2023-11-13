ARG NODE_VERSION=18.12.0

FROM node:${NODE_VERSION}-alpine AS node

FROM nginx:alpine

COPY --from=node /usr/lib /usr/lib
COPY --from=node /usr/local/lib /usr/local/lib
COPY --from=node /usr/local/include /usr/local/include
COPY --from=node /usr/local/bin /usr/local/bin

WORKDIR /app

RUN apk add --update apache2-utils
RUN apk add --update libwebp=1.3.2-r0
COPY package.json package-lock.json ./

RUN npm install


COPY . .

ENTRYPOINT ["/bin/sh", "/app/scripts/deploy.sh"]
