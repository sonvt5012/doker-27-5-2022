FROM nginx:alpine

RUN apk update \
    && apk upgrade \
    && apk add --no-cache --update \
        redis

CMD ["redis-server"]