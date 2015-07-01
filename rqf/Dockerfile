FROM debian:wheezy
MAINTAINER Paul Letkeman 
RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install -y\
    libsqlite3-dev\
    supervisor\
    git

ADD deb /root/deb
WORKDIR /root/deb
RUN dpkg -i mongrel2.deb
RUN dpkg -i zeromq.deb
RUN dpkg -i libsodium.deb
RUN ldconfig -n /usr/local/lib/ 
RUN ldconfig -v
WORKDIR /home/rqf
RUN git clone https://github.com/RealQuestions/frontend-v2.git frontend
WORKDIR /home/rqf/frontend
RUN mkdir run logs tmp
#RUN npm install
#RUN npm install -g gulp bower
#RUN bower install -F --allow-root
EXPOSE 80
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
CMD ["/usr/bin/supervisord"]
#RUN apt-get install -y \
