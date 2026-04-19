FROM alpine:3.20

WORKDIR /app

RUN apk add --no-cache python3 \
  && ln -sf /usr/bin/python3 /usr/local/bin/python \
  && addgroup -S app \
  && adduser -S -G app app \
  && find / -xdev \( -perm -4000 -o -perm -2000 \) -type f -exec chmod a-s {} +

COPY app.py /app/app.py

USER app
EXPOSE 8080

CMD ["python3", "/app/app.py"]

HEALTHCHECK --interval=10s --timeout=3s --start-period=5s --retries=3 \
  CMD python -c "import urllib.request; urllib.request.urlopen('http://127.0.0.1:8080/', timeout=2).read()" || exit 1
