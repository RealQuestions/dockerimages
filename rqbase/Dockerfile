FROM phusion/baseimage:0.9.16
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install --fix-missing -y \
    git \
    python \
    gcc \
    g++ \
    make


RUN mkdir /home/repositories
WORKDIR /home/repositories
RUN git clone https://github.com/joyent/node
WORKDIR /home/repositories/node
RUN git fetch
RUN git checkout v0.12.5
RUN ./configure
RUN make
RUN make install

CMD ["/usr/bin/supervisord"]

RUN apt-get install -y \
    supervisor
