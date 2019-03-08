FROM tomcat:8.5.15-jre8
MAINTAINER online-serviceApp

VOLUME /tmp

# Delete existing ROOT folder
RUN rm -rf /usr/local/tomcat/webapps/serviceApp

ADD ./target/shopizer.war /usr/local/tomcat/webapps/

ENV JAVA_OPTS="-Xmx1024m"

CMD ["catalina.sh", "run"]

EXPOSE 8080

