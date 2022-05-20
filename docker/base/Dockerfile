FROM ubuntu:xenial-20170802

LABEL maintainer=""

ENV DEBIAN_FRONTEND=noninteractive

COPY apt-conf /etc/apt/apt.conf.d/

RUN apt-get update && \
    apt-get install autoconf \
                    python3-dev \
                    python-dev \
                    libiberty-dev \
                    build-essential \
                    make
ENTRYPOINT [\
  "distccd", \
  "--daemon", \
  "--no-detach", \
  "--user", "distcc", \
  "--port", "3632", \
  "--stats", \
  "--stats-port", "3633", \
  "--log-stderr", \
  "--listen", "0.0.0.0"\
]
