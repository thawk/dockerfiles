FROM alpine:3.8

ARG VERSION

LABEL maintainer="zgist" \
        org.label-schema.name="MariaDB" \
        org.label-schema.version=$VERSION

RUN set -ex && \
    apk add --no-cache bash mariadb mariadb-client tzdata && \
    mkdir -p /run/mysqld && \
    chown mysql:mysql /run/mysqld && \
    sed -Ei -e 's/^(bind-address|log)/#&/' \
        -e 's/^\[mysqld\]$/&\nskip-host-cache\nskip-name-resolve\nuser=mysql/' /etc/mysql/my.cnf

COPY docker-entrypoint.sh /

EXPOSE 3306

VOLUME ["/var/lib/mysql"]

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["mysqld"]
