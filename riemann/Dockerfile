FROM openjdk:12-alpine

MAINTAINER Matthias Varberg Ingesman, matthias@ingesman.dk

## install riemann
ENV RIEMANN_VERSION 0.3.1
RUN wget https://github.com/riemann/riemann/releases/download/$RIEMANN_VERSION/riemann-$RIEMANN_VERSION.tar.bz2 && \
  tar xvjf riemann-$RIEMANN_VERSION.tar.bz2 && \
  mv /riemann-$RIEMANN_VERSION /app

WORKDIR /app

## hack shell wrapper to use busybox sh
RUN sed -ie 's/env bash/env sh/' bin/riemann

## hack default config to listen on all interfaces
RUN sed -ie 's/127.0.0.1/0.0.0.0/' etc/riemann.config

EXPOSE 5555/tcp 5555/udp 5556

CMD [ "bin/riemann", "etc/riemann.config" ]
