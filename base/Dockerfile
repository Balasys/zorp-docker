FROM ubuntu:19.10

MAINTAINER Szilárd Pfeiffer "coroner@pfeifferszilard.hu"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
 && apt-get install -y --no-install-recommends gpg-agent gnupg2 \
 && apt-key adv --fetch-keys http://download.opensuse.org/repositories/security:/Zorp:/7:/0:/5/xUbuntu_19.10/Release.key \
 && echo "deb http://download.opensuse.org/repositories/security:/Zorp:/7:/0:/5/xUbuntu_19.10/ ./" >/etc/apt/sources.list.d/zorp.list \
 && apt-get update

RUN apt-get install -y \
    zorp \
    zorp-modules \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && rm -rf /var/tmp/* \
 && rm -rf /tmp/*

ENV ZORP_CONFIG_DIR /etc/zorp/
ADD policy.py $ZORP_CONFIG_DIR/policy.py

COPY . /app/

ENTRYPOINT ["/app/docker-entrypoint.sh"]
CMD [ \
     "/usr/sbin/zorp", \
     "--foreground", \
     "--no-syslog", \
     "--user", "zorp", \
     "--group", "zorp", \
     "--verbose", "3", \
     "--log-spec", "*.accounting:4,core.summary:4", \
     "--as", "default" \
    ]
