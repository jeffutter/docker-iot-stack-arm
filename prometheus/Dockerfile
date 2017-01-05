FROM container4armhf/armhf-alpine:3.4

ENV VERSION=1.4.1

RUN apk add --no-cache --virtual .build-deps \
      curl \
    && curl -o prometheus.tar.gz -sSL https://github.com/prometheus/prometheus/releases/download/v${VERSION}/prometheus-${VERSION}.linux-armv6.tar.gz \
    && tar -zxf prometheus.tar.gz \
    && mkdir -p /etc/prometheus \
    && mv prometheus-${VERSION}.linux-armv6/prometheus /bin/prometheus \
    && mv prometheus-${VERSION}.linux-armv6/promtool /bin/promtool \
    && mv prometheus-${VERSION}.linux-armv6/prometheus.yml /etc/prometheus/prometheus.yml \
    && mv prometheus-${VERSION}.linux-armv6/console_libraries /etc/prometheus/ \
    && mv prometheus-${VERSION}.linux-armv6/consoles /etc/prometheus/ \
    && rm -rf prometheus.tar.gz prometheus-${VERSION}.linux-armv6 \
    && apk del .build-deps

EXPOSE     9090
VOLUME     [ "/prometheus" ]
WORKDIR    /prometheus
ENTRYPOINT [ "/bin/prometheus" ]
CMD        [ "-config.file=/etc/prometheus/prometheus.yml", \
             "-storage.local.path=/prometheus", \
             "-web.console.libraries=/etc/prometheus/console_libraries", \
             "-web.console.templates=/etc/prometheus/consoles" ]
