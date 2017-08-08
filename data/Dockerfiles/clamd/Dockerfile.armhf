FROM resin/armhf-alpine:3.6

LABEL maintainer "Adrien Girardeau <adigir25@gmail.com>"

RUN [ "cross-build-start" ]

# Add scripts
COPY dl_files.sh bootstrap.sh ./

# Installation
RUN apk add --update \
	&& apk add --no-cache clamav clamav-libunrar curl bash \
	&& chmod +x /dl_files.sh \
	&& set -ex; /bin/bash /dl_files.sh \
	&& mkdir /run/clamav \
	&& chown clamav:clamav /run/clamav \
	&& chmod 750 /run/clamav \
	&& sed -i '/Foreground yes/s/^#//g' /etc/clamav/clamd.conf \
	&& sed -i '/TCPSocket 3310/s/^#//g' /etc/clamav/clamd.conf \
	&& sed -i '/Foreground yes/s/^#//g' /etc/clamav/freshclam.conf

RUN [ "cross-build-end" ]

# Port provision
EXPOSE 3310

# AV daemon bootstrapping
CMD ["/bootstrap.sh"]
