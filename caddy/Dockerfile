FROM caddy:2.3.0-builder-alpine AS builder

RUN xcaddy build \
    --with github.com/mholt/caddy-webdav@c949b32

FROM caddy:2.3.0-alpine

COPY --from=builder /usr/bin/caddy /usr/bin/caddy

