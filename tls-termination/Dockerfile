FROM balasys/zorpgpl:7.0.2

MAINTAINER Szilárd Pfeiffer "coroner@pfeifferszilard.hu"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update
RUN apt-get install -y \
    openssl \
 && rm -rf /var/lib/apt/lists/*

ADD policy.py $ZORP_CONFIG_DIR/policy.py

COPY . /app/

EXPOSE 443
