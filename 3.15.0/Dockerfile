# Gatling is a highly capable load testing tool.
#
# Documentation: https://gatling.io/docs/3.2/
# Cheat sheet: https://gatling.io/docs/3.2/cheat-sheet/

FROM amazoncorretto:25-alpine-jdk

MAINTAINER Nadezhda Ryabtsova <nadezhdaryabtsova@gmail.com>

# gating version
ENV GATLING_VERSION 3.15.0

# working directory for gatling
WORKDIR /opt/

# install gatling
RUN mkdir -p gatling && \
    apk upgrade --update-cache --available && \
    apk add --update wget bash libc6-compat openssl openssl-dev && \
    mkdir -p /tmp/downloads && \
    wget -q -O /tmp/downloads/gatling-$GATLING_VERSION.zip \
    https://repo1.maven.org/maven2/io/gatling/highcharts/gatling-charts-highcharts-bundle/$GATLING_VERSION/gatling-charts-highcharts-bundle-$GATLING_VERSION-bundle.zip && \
    mkdir -p /tmp/archive && cd /tmp/archive && \
    unzip /tmp/downloads/gatling-$GATLING_VERSION.zip && \
    cd /tmp/archive/gatling-charts-highcharts-bundle-$GATLING_VERSION/ && \
    mv $(ls -a1 | sed "/\.$/d" | sed "/\.\.$/d") /opt/gatling/ && \
    rm -rf /tmp/* && \
    rm -rf /var/cache/apk/*

# change context to gatling directory
WORKDIR  /opt/gatling

# set directories below to be mountable from host
VOLUME ["/opt/gatling/conf", "/opt/gatling/results", "/opt/gatling/user-files"]

# set environment variables
ENV PATH /opt/gatling/bin:/opt/gatling:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV GATLING_HOME /opt/gatling

ENTRYPOINT ["mvnw", "gatling:test"]
