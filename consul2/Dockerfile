FROM tsuyukimakoto/consul
MAINTAINER tsuyukimakoto

RUN mkdir -p /etc/consul/conf.d
ADD ./tmpl/nginx.json /etc/consul/conf.d/nginx.json

# Consul port -> DNS HTTP RPC SERF_LAN SERF_WAN SERVER
EXPOSE 22 80 8600/tcp 8600/udp 8500/tcp 8500/udp 8400/tcp 8400/udp 8301/tcp 8301/udp 8302/tcp 8302/udp 8300/tcp 8300/udp

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
