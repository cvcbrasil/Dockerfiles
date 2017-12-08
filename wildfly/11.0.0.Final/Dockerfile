FROM cvcbrasil/java:8u141-jre

LABEL cvc.com.br.version="1.0" \
      vendor="CVC Brasil S.A." \
      cvc.com.br.release-date="2017-12-06"

ENV WILDFLY_VERSION 11.0.0.Final
ENV JBOSS_HOME /opt/jboss/wildfly
ENV STANDALONE standalone

USER root
RUN mkdir -p /opt/jboss \
    && adduser -D -h /opt/jboss jboss \
    && apk add --no-cache curl 

USER jboss
WORKDIR /opt/jboss
RUN curl -O http://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.zip \
    && unzip wildfly-$WILDFLY_VERSION.zip \
    && mv $HOME/wildfly-$WILDFLY_VERSION $HOME/wildfly \
    && rm wildfly-$WILDFLY_VERSION.zip

