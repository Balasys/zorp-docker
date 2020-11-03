FROM balasys/zorpgpl:7.0.6

MAINTAINER Szilárd Pfeiffer "coroner@pfeifferszilard.hu"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
    devscripts \
    equivs \
    git-core \
    ca-certificates
RUN git clone -b 7.0.6.0 https://github.com/Balasys/libzorpll.git /usr/src/libzorpll \
 && git clone -b 7.0.6 https://github.com/Balasys/zorp.git /usr/src/zorp \
 && mk-build-deps -i -t "apt-get -o Debug::pkgProblemResolver=yes --yes --no-install-recommends" /usr/src/libzorpll/debian/control \
 && mk-build-deps -i -t "apt-get -o Debug::pkgProblemResolver=yes --yes --force-yes --no-install-recommends" /usr/src/zorp/debian/control
RUN apt-get autoremove -y \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && rm -rf /var/tmp/* \
 && rm -rf /tmp/*

RUN cd /usr/src/libzorpll \
 && autoreconf -if \
 && ./configure --enable-debug \
    --prefix=/usr \
    --mandir=/usr/share/man \
    --infodir=/usr/share/info \
    --sysconfdir=/etc \
    --libexecdir=/usr/libzorpll \
 && make -j \
 && make check -j \
 && make install

RUN cd /usr/src/zorp \
 && autoreconf -if \
 && ./configure --enable-debug \
    --prefix=/usr \
    --mandir=/usr/share/man \
    --infodir=/usr/share/info \
    --localstatedir=/var/lib/zorp \
    --sysconfdir=/etc \
    --with-pidfiledir=/var/run/zorp/ \
 && make -j \
 && make check -j \
 && make install
