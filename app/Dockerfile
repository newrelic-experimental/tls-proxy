# JDK 11.0.10 is intentional; this version still permits TLSv1 and TLSv1.1
FROM openjdk:11.0.10-jre
WORKDIR /tmp
USER root
COPY spring-petclinic-2.7.3.jar app.jar
RUN wget --quiet https://download.newrelic.com/newrelic/java-agent/newrelic-agent/7.11.1/newrelic-agent-7.11.1.jar
COPY newrelic.yml /tmp
ENV NEW_RELIC_LOG_FILE_NAME="STDOUT"
ENTRYPOINT ["java","-javaagent:/tmp/newrelic-agent-7.11.1.jar","-Djdk.tls.server.protocols=TLSv1","-Djdk.tls.client.protocols=TLSv1","-jar","/tmp/app.jar"]
# TLS DEBUG: very verbose
#ENTRYPOINT ["java","-javaagent:/tmp/newrelic-agent-7.11.1.jar","-Djdk.tls.server.protocols=TLSv1","-Djdk.tls.client.protocols=TLSv1","-Djavax.net.debug=all","-jar","/tmp/app.jar"]
# happy-path uses JVM default of TLSv1.2
#ENTRYPOINT ["java","-javaagent:/tmp/newrelic-agent-7.11.1.jar","-jar","/tmp/app.jar"]
