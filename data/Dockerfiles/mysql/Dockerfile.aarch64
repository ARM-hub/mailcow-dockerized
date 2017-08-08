FROM resin/aarch64-alpine:3.6

LABEL maintainer "Adrien Girardeau <adigir25@gmail.com>"

RUN [ "cross-build-start" ]

# add gosu for easy step-down from root
ENV GOSU_VERSION 1.7
RUN set -x \
	&& apk add --no-cache ca-certificates wget gnupg \
	&& wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-arm64" \
	&& wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-arm64.asc" \
	&& export GNUPGHOME="$(mktemp -d)" \
	&& gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
	&& gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \
	&& rm -r "$GNUPGHOME" /usr/local/bin/gosu.asc \
	&& chmod +x /usr/local/bin/gosu \
	&& gosu nobody true \
	&& apk remove ca-certificates wget gnupg

RUN mkdir /docker-entrypoint-initdb.d

# install "pwgen" for randomizing passwords
RUN apk add --no-cache pwgen

VOLUME /var/lib/mysql

COPY docker-entrypoint.sh /usr/local/bin/

RUN ln -s usr/local/bin/docker-entrypoint.sh / # backwards compat

RUN [ "cross-build-end" ]

EXPOSE 3306

ENTRYPOINT ["docker-entrypoint.sh"]

CMD ["mysqld"]
