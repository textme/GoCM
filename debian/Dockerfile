FROM dotdeb/debian:wheezy-amd64
MAINTAINER Guillaume Plessis "gui@dotdeb.org"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get dist-upgrade -y

RUN apt-get install -y build-essential devscripts equivs libwww-perl \
    && apt-get install -y -t wheezy-backports dh-golang golang-go

ADD debian/control /root/
RUN mk-build-deps --install --tool 'apt-get -y' --remove /root/control && rm -f /root/control

ADD . /usr/src/builddir
WORKDIR /usr/src/builddir

#RUN uscan --download-current-version
RUN dpkg-buildpackage -b

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/src/builddir
