FROM caddy:2 AS caddy

FROM ghost:6

COPY --from=caddy /usr/bin/caddy /usr/bin/caddy
COPY ./Caddyfile /etc/caddy/Caddyfile
COPY ./snippets/ /etc/caddy/snippets/

RUN chown -R node:node /etc/caddy

RUN set -eux; \
    apt-get update; \
    apt-get install -y --no-install-recommends supervisor; \
    rm -rf /var/lib/apt/lists/*

COPY ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 8080

CMD ["/usr/bin/supervisord","-c","/etc/supervisor/conf.d/supervisord.conf"]