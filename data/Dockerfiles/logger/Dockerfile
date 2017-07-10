FROM debian:stretch-slim
LABEL maintainer "Frank Werner-Krippendorf <mail@hb9fxq.ch>"

ARG DEBIAN_FRONTEND=noninteractive
ENV LC_ALL C

RUN dpkg-divert --local --rename --add /sbin/initctl \
	&& ln -sf /bin/true /sbin/initctl \
	&& dpkg-divert --local --rename --add /usr/bin/ischroot \
	&& ln -sf /bin/true /usr/bin/ischroot

RUN apt-get update && apt-get install -y --no-install-recommends \
	ca-certificates \
	curl \
	ncdu \
	dfc \
	dirmngr \
	gnupg \
	libsasl2-modules \
	sudo \
	supervisor \
	syslog-ng \
	pflogsumm \
	logrotate \
	syslog-ng-core \
	syslog-ng-mod-redis \
	&& rm -rf /var/lib/apt/lists/*

RUN touch /etc/default/locale

COPY supervisord.conf /etc/supervisor/supervisord.conf
COPY logger.sh /opt/logger.sh

CMD exec /usr/bin/supervisord -c /etc/supervisor/supervisord.conf

RUN rm -rf /tmp/* /var/tmp/*
