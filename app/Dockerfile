FROM openjdk:12-ea-13-jdk-oraclelinux7
WORKDIR /tmp
USER root
COPY spring-petclinic-2.7.3.jar app.jar
RUN yum install -y wget
RUN wget https://download.newrelic.com/newrelic/java-agent/newrelic-agent/7.10.0/newrelic-agent-7.10.0.jar
ADD newrelic.yml /tmp
ENV NEW_RELIC_LOG_FILE_NAME="STDOUT"
ENTRYPOINT ["java","-javaagent:/tmp/newrelic-agent-7.10.0.jar","-Djdk.tls.server.protocols=TLSv1","-Djdk.tls.client.protocols=TLSv1","-jar","/tmp/app.jar"]
