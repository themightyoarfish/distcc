FROM ubuntu:20.04

LABEL maintainer=""

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y autoconf \
                    python3-dev \
                    python-dev \
                    libiberty-dev \
                    build-essential \
                    make
COPY . /distcc
WORKDIR /distcc

RUN ./autogen.sh && ./configure && make clean && make && make install

RUN useradd -s /bin/bash distcc
RUN touch /var/log/distccd.log
RUN chown distcc:root /var/log/distccd.log

RUN apt-get update && \
    apt-get -y install clang && \
    apt-get remove -y gcc g++

RUN update-distcc-symlinks

RUN apt-get update && \
    apt-get -y install htop

ENTRYPOINT [\
  "distccd", \
  "--daemon", \
  "--no-detach", \
  "--user", "distcc", \
  "--port", "3632", \
  "--stats", \
  "--stats-port", "3633", \
  "--verbose", \
  "--log-level", "debug", \
  "--log-stderr", \
  "--listen", "0.0.0.0", \
  "--enable-tcp-insecure", \
  "--jobs", "20" \
]
