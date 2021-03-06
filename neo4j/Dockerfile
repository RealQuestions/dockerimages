FROM debian
MAINTAINER Erle Pereira <erle@erlepereira.com>

ENV DEBIAN_FRONTEND=noninteractive
ENV neohome /usr/local/neo4j-server
ENV neolib /var/lib/neo4j-server

RUN apt-get update 

RUN \
	apt-get install -y software-properties-common python-software-properties lsof && \
	echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
	add-apt-repository -y ppa:webupd8team/java && \
	sed -i 's/jessie/vivid/g' /etc/apt/sources.list.d/webupd8team-java-jessie.list && \
	apt-get update && \
	apt-get install -y oracle-java7-installer && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /var/cache/oracle-jdk9-installer && \
	cd /tmp && \
	wget http://neo4j.com/artifact.php?name=neo4j-community-2.2.2-unix.tar.gz -O neo4j.tar.gz && \
	useradd neo4j -m -d ${neohome} && \
	cd /tmp && \
	mkdir neo4j && \
	tar -zxf neo4j.tar.gz -C ./ && \
	rm neo4j.tar.gz && \
	mv neo4j-community-2.2.2/* ${neohome} && \
	ln -s ${neohome}/bin/neo4j /usr/local/bin/neo4j && \
	mkdir ${neolib} && \
	chown -R neo4j:neo4j ${neohome} && \
	chown -R neo4j:neo4j ${neolib}

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
