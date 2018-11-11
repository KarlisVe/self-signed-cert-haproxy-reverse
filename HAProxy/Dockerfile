FROM haproxy:latest

COPY haproxy.cfg /usr/local/etc/haproxy/haproxy.cfg

COPY certs/proxytst.pem /private/proxytest.pem

RUN groupadd haproxy && useradd -g haproxy haproxy

RUN mkdir -p /var/lib/haproxy/run/haproxy/