FROM rqbase
MAINTAINER Paul Letkeman 
RUN apt-get update -y
RUN apt-get upgrade -y
WORKDIR /home/rqf
RUN git clone https://github.com/RealQuestions/frontend-v2.git frontend
WORKDIR /home/rqf/frontend
RUN npm install
RUN npm install -g gulp bower
RUN bower install -F --allow-root
EXPOSE 9090
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
CMD ["/usr/bin/supervisord"]
#RUN apt-get install -y \
