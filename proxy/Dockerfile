FROM debian:11.5 AS build
RUN apt-get -y update
RUN apt-get install -y curl git openssl  build-essential libssl-dev wget vim curl
WORKDIR /apps/
RUN wget -O - http://www.squid-cache.org/Versions/v5/squid-5.7.tar.gz | tar zxfv - \
    && CPU=$(( `nproc --all`-1 )) \
    && cd /apps/squid-5.7/ \
    && ./configure --prefix=/apps/squid --enable-icap-client --enable-ssl --with-openssl --enable-ssl-crtd --enable-auth --enable-basic-auth-helpers="NCSA" --with-pidfile=/var/run/squid-X.pid \
    && make -j$CPU \
    && make install \
    && cd /apps \
    && rm -rf /apps/squid-5.7

COPY openssl.cnf /etc/ssl/openssl.cnf
ADD default_squid_config.conf /apps/default_squid_config.conf

RUN chown -R nobody:nogroup /apps/
RUN mkdir -p  /apps/squid/var/lib/
RUN mkdir -p  /squid/var/cache/squid
RUN /apps/squid/libexec/security_file_certgen -c -s /apps/squid/var/cache/squid/ssl_db -M 20MB 
RUN /apps/squid/sbin/squid -N -f /apps/default_squid_config.conf -z
RUN chown -R nobody:nogroup /apps/
RUN chgrp -R 0 /apps && chmod -R g=u /apps

EXPOSE 3128
