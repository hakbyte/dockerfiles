# Caddy + WebDAV

Official [Caddy 2.3.0](https://hub.docker.com/_/caddy?tab=description) image with a few customizations:

- WebDAV module enabled: https://github.com/mholt/caddy-webdav
- Added tzdata package (support to timezones via `TZ` environment variable)

Minimal docker-compose example with timezone set to Europe/Berlin (find your timezone [here](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)):

```yml
version: "3.8"

services:
  caddy:
    image: hakbyte/caddy
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - $PWD/Caddyfile:/etc/caddy/Caddyfile
      - caddy-data:/data
      - caddy-config:/config
      - webdav:/webdav
    environment:
      - TZ=Europe/Berlin
volumes:
  caddy-data:
  caddy-config:
  webdav:
```

Caddyfile:

```
mydomain.com {
    route {
        webdav {
            root /webdav
        }
    }
}
```