FROM rqf_test
MAINTAINER Paul Letkeman 
RUN apt-get update -y
RUN apt-get upgrade -y
WORKDIR /home/rqf
RUN git clone https://github.com/RealQuestions/frontend-v2.git frontend
WORKDIR /home/rqf/frontend
RUN npm install
EXPOSE 9090
CMD gulp serve
// RUN apt-get install -y \




