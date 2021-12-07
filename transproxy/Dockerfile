FROM ubuntu:20.04

WORKDIR /app
RUN set +x \
    && apt-get update \
    && apt-get install -y \
        curl \
        iptables \
        iproute2 \
        iputils-ping \
        net-tools \
        dnsutils \
        ulogd2 \
        curl \
    && curl \
        -sSL \
        --output go-transproxy.tar.gz \
        https://github.com/wadahiro/go-transproxy/releases/download/v0.5.2/go-transproxy-0.5.2.tar.gz \
    # && : # todo: checksum \
    && tar -xzvf go-transproxy.tar.gz \
    && cp bin/transproxy /usr/local/bin \
    && rm -rf /app/**

RUN sed -i -e 's/#net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/' /etc/sysctl.conf
RUN sed -i -e 's/#net.ipv4.conf.all.send_redirects = 0/net.ipv4.conf.all.send_redirects = 0/' /etc/sysctl.conf

CMD ["sh", "-c", "iptables -t nat -A POSTROUTING -j MASQUERADE && transproxy" ]
