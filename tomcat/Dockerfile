FROM centos:7

RUN yum -y update && yum install -y wget && yum install -y tar

ENV JAVA_HOME /opt/java
ENV CATALINA_HOME /opt/tomcat 
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/bin:$CATALINA_HOME/scripts

RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" \
        http://download.oracle.com/otn-pub/java/jdk/7u71-b14/jdk-7u71-linux-x64.tar.gz &&\
        tar -xvf jdk-7u71-linux-x64.tar.gz && \
        rm jdk-7u71-linux-x64.tar.gz && \
        mv jdk* ${JAVA_HOME}

RUN wget http://apache-mirror.rbc.ru/pub/apache/tomcat/tomcat-8/v8.5.0/bin/apache-tomcat-8.5.0.tar.gz && \
        tar -xvf apache-tomcat-8.5.0.tar.gz && \
        rm apache-tomcat-8.5.0.tar.gz && \
        mv apache* ${CATALINA_HOME}

RUN chmod +x ${CATALINA_HOME}/bin/*sh

# Create tomcat user
RUN groupadd -r tomcat && \
	useradd -g tomcat -d ${CATALINA_HOME} -s /sbin/nologin  -c "Tomcat user" tomcat && \
	chown -R tomcat:tomcat ${CATALINA_HOME}

WORKDIR /opt/tomcat

EXPOSE 8080
EXPOSE 8009

USER tomcat
CMD ["exec bin/catalina.sh run"]