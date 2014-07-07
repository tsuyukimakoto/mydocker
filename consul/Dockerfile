FROM ubuntu
MAINTAINER tsuyukimakoto

RUN apt-get -qq update
RUN apt-get install -yqq wget unzip openssh-server nginx supervisor
RUN mkdir -p /var/run/sshd
RUN mkdir -p /var/log/supervisor
RUN mkdir -p /root/.ssh
RUN chmod 700 /root/.ssh
ADD ./tmpl/id_rsa.pub /root/.ssh/authorized_keys
ADD ./tmpl/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
RUN sed -ri 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config
RUN chmod -R g-rwx,o-rwx /root/.ssh
RUN sed -ri "s/user www-data;/user root;/g" /etc/nginx/nginx.conf
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN wget https://dl.bintray.com/mitchellh/consul/0.3.0_linux_amd64.zip
RUN unzip 0.3.0_linux_amd64.zip && mv consul /tmp/consul
# Consul port -> DNS HTTP RPC SERF_LAN SERF_WAN SERVER
EXPOSE 22 80 8600/tcp 8600/udp 8500/tcp 8500/udp 8400/tcp 8400/udp 8301/tcp 8301/udp 8302/tcp 8302/udp 8300/tcp 8300/udp

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
