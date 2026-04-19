FROM alpine:3.20

WORKDIR /etc/nginx

RUN apk add --no-cache \
    nginx \
    ca-certificates \
    curl \
  && rm -rf /etc/nginx/http.d/* /etc/nginx/conf.d/* 2>/dev/null || true \
  && mkdir -p /tmp/nginx/client_temp /tmp/nginx/proxy_temp /tmp/nginx/fastcgi_temp /tmp/nginx/uwsgi_temp /tmp/nginx/scgi_temp \
  && chown -R nginx:nginx /tmp/nginx \
  && find / -xdev \( -perm -4000 -o -perm -2000 \) -type f -exec chmod a-s {} +

COPY --chown=root:root --chmod=0644 nginx.conf /etc/nginx/nginx.conf

USER nginx
EXPOSE 8080

CMD ["/usr/sbin/nginx", "-g", "daemon off;"]

HEALTHCHECK --interval=10s --timeout=3s --start-period=5s --retries=3 \
  CMD curl -fsS http://127.0.0.1:8080/ >/dev/null || exit 1
