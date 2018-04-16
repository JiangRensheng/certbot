FROM ubuntu:16.04

ENTRYPOINT [ "certbot" ]
EXPOSE 80 443
VOLUME /etc/letsencrypt /var/lib/letsencrypt
WORKDIR /opt/certbot

RUN apt-get update
RUN sed 's|http://cn.archive.ubuntu.com|https://mirrors.aliyun.com|g;s|http://security.ubuntu.com|https://mirrors.aliyun.com|g' /etc/apt/sources.list
RUN apt-get update


COPY CHANGES.rst README.rst setup.py src/
COPY acme src/acme
COPY certbot src/certbot

RUN apt-get install -yqq \
        libffi6 \
        libssl1.0 \
        openssl \
        ca-certificates \
        binutils

RUN apt-get install -yqq \
        gcc \
        linux-headers-$(uname -r) \
        libssl-dev \
        musl-dev \
        libffi-dev 

RUN apt-get install -yqq \
        python python-pip \
        apache2 nginx \
        python-letsencrypt-apache 

RUN pip install --upgrade pip

RUN pip install --no-cache-dir \
        --editable /opt/certbot/src/acme \
        --editable /opt/certbot/src 
