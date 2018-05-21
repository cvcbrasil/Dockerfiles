FROM cvcbrasil/java:8u141-jre

LABEL cvc.com.br.version="1.0" \
      vendor="CVC Brasil S.A." \
      cvc.com.br.release-date="2018-02-05"

ENV WILDFLY_VERSION 8.2.0.Final
ENV JBOSS_HOME /opt/jboss/wildfly
ENV STANDALONE standalone
ENV LOGSTASH_GELF_VERSION 1.11.2
ENV ORACLE_JDBC_VERSION 121010

USER root
RUN mkdir -p /opt/jboss \
    && adduser -D -h /opt/jboss jboss \
    && apk add --no-cache curl 

USER jboss

WORKDIR /opt/jboss

RUN curl -O http://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.zip \
    && unzip wildfly-$WILDFLY_VERSION.zip \
    && mv $HOME/wildfly-$WILDFLY_VERSION $HOME/wildfly \
    && rm wildfly-$WILDFLY_VERSION.zip \
    && curl -O http://search.maven.org/remotecontent?filepath=biz/paluch/logging/logstash-gelf/$LOGSTASH_GELF_VERSION/logstash-gelf-$LOGSTASH_GELF_VERSION-logging-module.zip \
    && unzip logstash-gelf-$LOGSTASH_GELF_VERSION-logging-module.zip \
    && mv $HOME/logstash-gelf-$LOGSTASH_GELF_VERSION/biz $HOME/wildfly/modules/system/layers/base \
    && rm -r logstash-gelf-$LOGSTASH_GELF_VERSION-logging-module.zip logstash-gelf-$LOGSTASH_GELF_VERSION \
    && mkdir -p $HOME/wildfly/modules/system/layers/base/com/oracle/main

COPY --chown=jboss:jboss oracle_jdbc/* /opt/jboss/wildfly/modules/system/layers/base/com/oracle/main/



