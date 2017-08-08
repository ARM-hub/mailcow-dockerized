FROM resin/armhf-alpine:3.6

RUN [ "cross-build-start" ]

LABEL maintainer "Adrien Girardeau <adigir25@gmail.com>"

RUN apk add --update --no-cache \
	bash \
	acme-client \
	curl \
	openssl \
	bind-tools \
	jq \
	mariadb-client

COPY docker-entrypoint.sh /srv/docker-entrypoint.sh

RUN [ "cross-build-end" ]

ENTRYPOINT ["/srv/docker-entrypoint.sh"]
