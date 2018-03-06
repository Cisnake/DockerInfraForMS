### Base image we use to create our image from
FROM jenkins/jenkins

### info about 
### MAINTAINER atlas-team (email)

### get rid of admin password setup
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"

### automatically installing plugins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

USER root
### create folders for maven & JDK
RUN mkdir /usr/share/jenkins/ref/downloads && \
	mkdir /tools

#RUN curl "http://mirror.vorboss.net/apache/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz" > /usr/share/jenkins/ref/downloads/apache-maven-3.5.2-bin.tar.gz
#RUN curl "http://ftp.osuosl.org/pub/funtoo/distfiles/oracle-java/jdk-8u144-linux-x64.tar.gz" > /usr/share/jenkins/ref/downloads/jdk-8u144-linux-x64.tar.gz
### use copy instead of downloads
## Cette comande pour eviter le tekechargement depuis internet ... A supprimer 
COPY downloads/apache-maven-3.5.2-bin.tar.gz /usr/share/jenkins/ref/downloads/apache-maven-3.5.2-bin.tar.gz
COPY downloads/jdk-8u144-linux-x64.tar.gz /usr/share/jenkins/ref/downloads/jdk-8u144-linux-x64.tar.gz

RUN cd /usr/share/jenkins/ref/downloads && \
	tar xzvf jdk-8u144-linux-x64.tar.gz -C /tools && \
	tar xzvf apache-maven-3.5.2-bin.tar.gz -C /tools

	
	
### copy maven settings file
RUN cd /tools && \
	mkdir -m 777 maven_repository

USER jenkins
COPY settings.xml /tools/apache-maven-3.5.2/conf/settings.xml	

COPY groovy/* /usr/share/jenkins/ref/init.groovy.d/
#COPY config/credentials.xml /var/jenkins_home/credentials.xml
#RUN cd /var/jenkins_home && \
#	mkdir users/admin && \
#	cp config/admin.xml users/admin/config.xml
#RUN cd /var/jenkins_home/jobs && \
#	mkdir Multi_branche_test/indexing
#	cp config/ Multi_branche_test/config.xml

#USER root
#
## Install Docker from official repo
#RUN apt-get update -qq && \
#    apt-get install -qqy apt-transport-https ca-certificates curl gnupg2 software-properties-common && \
#    curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
#    apt-key fingerprint 0EBFCD88 && \
#    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" && \
#    apt-get update -qq && \
#    apt-get install -qqy docker-ce && \
#    usermod -aG docker jenkins && \
#    chown -R jenkins:jenkins $JENKINS_HOME/
#
#USER jenkins

#VOLUME [$JENKINS_HOME, "/var/run/docker.sock"]
