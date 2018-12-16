FROM ubuntu:16.04

MAINTAINER Adam Czyzynski <adam.czyzynski@enxoo.com>

# Install Java.
RUN \
        echo "current version of java available: 8u45+8u33arm-1~webupd8~0" && \
        echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee /etc/apt/sources.list.d/webupd8team-java.list && \
        echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list && \
        apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 && \
        echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
        apt-get update -qqy && \
        apt-get install -y oracle-java8-installer && \
	apt-get install oracle-java8-set-default && \
	apt-get install -y jq && \
	apt-get install -y postgresql-client && \
        rm -rf /var/lib/apt/lists/* && \
        rm -rf /var/cache/oracle-jdk8-installer \
        ;
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# Add mule
RUN \ 
	adduser mule && \
	usermod -s /bin/bash -d /home/mule -a -G sudo mule && \
	wget https://repository-master.mulesoft.org/nexus/content/repositories/releases/org/mule/distributions/mule-standalone/3.8.0/mule-standalone-3.8.0.tar.gz && \
	tar -xf mule-standalone-3.8.0.tar.gz -C /opt/ && \
	chown -R mule /opt/mule-standalone-3.8.0 && \
	chmod -R u+rX /opt/mule-standalone-3.8.0 && \
	export MULE_HOME=/opt/mule-standalone-3.8.0 && \
	export PATH=$PATH:$MULE_HOME/bin \
	;
EXPOSE 1098/tcp
EXPOSE 1099/tcp
EXPOSE 8899/tcp
EXPOSE 7777/tcp
EXPOSE 1998/tcp
EXPOSE 7001
EXPOSE 8081
COPY swagger /home/mule/swagger
VOLUME ["/opt/mule-standalone-3.8.0/apps/", "/opt/mule-standalone-3.8.0/logs/"]
RUN echo "wrapper.java.additional.15=-Dmule.encoding=UTF-8" >> /opt/mule-standalone-3.8.0/conf/wrapper.conf
RUN ln -s /opt/mule-standalone-3.8.0 /opt/mule
COPY configuration/mule.service /usr/lib/systemd/system/mule.service
CMD [ "/opt/mule/bin/mule"]

