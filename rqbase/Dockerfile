FROM phusion/baseimage:0.9.16
RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install --fix-missing -y \
    git \
    python \
    GCC \
    g++ \
    make


RUN mkdir /home/repositories
WORKDIR /home/repositories
RUN git clone https://github.com/joyent/node
WORKDIR /home/repositories/node
RUN ./configure
RUN make
RUN make install

CMD ["/usr/bin/supervisord"]

RUN apt-get install -y \
    supervisor
