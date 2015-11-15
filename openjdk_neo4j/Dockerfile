FROM alpine
MAINTAINER Erle Pereira <erle@erlepereira.com>

ENV neohome /usr/local/neo4j-server
ENV neolib /var/lib/neo4j-server

RUN apk --update add openjdk7-jre-base wget bash

RUN wget http://neo4j.com/artifact.php?name=neo4j-community-2.1.8-unix.tar.gz -O /tmp/neo4j.tar.gz && \
	adduser -h ${neohome} -S neo4j && \
	addgroup neo4j && \
	cd /tmp && \
	mkdir neo4j && \
	tar -zxf neo4j.tar.gz -C ./ && \
	rm neo4j.tar.gz && \
	mv neo4j-community-2.1.8/* ${neohome} && \
	ln -s ${neohome}/bin/neo4j /usr/local/bin/neo4j && \
	mkdir ${neolib} && \
	chown -R neo4j:neo4j ${neohome} && \
	chown -R neo4j:neo4j ${neolib}

#RUN apk add maven --update-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/ 

RUN cd ${neohome}/plugins && \
    wget https://github.com/thinkaurelius/neo4j-gremlin-plugin/releases/download/2.1.6/neo4j-gremlin-plugin-tp2-2.1.6-server-plugin.zip --no-check-certificate && \
    unzip neo4j-gremlin-plugin-tp2-2.1.6-server-plugin.zip

VOLUME ${neolib}

ADD etc/init.d/neo4j /etc/init.d/neo4j
ADD conf/neo4j-server.properties ${neohome}/conf/neo4j-server.properties
ADD conf/neo4j.properties ${neohome}/conf/neo4j.properties
ADD conf/neo4j-wrapper.conf ${neohome}/conf/neo4j-wrapper.conf
ADD conf/neo4j.conf /etc/security/limits.d/neo4j.conf

RUN chmod +x /etc/init.d/neo4j

USER neo4j

EXPOSE 7474
ENTRYPOINT ["neo4j", "console"]
