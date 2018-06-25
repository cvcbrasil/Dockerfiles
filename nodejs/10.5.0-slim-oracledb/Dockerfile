FROM cvcbrasil/nodejs:10.5.0-slim

ENV ORACLE_VERSION_MAJOR=12 \
    ORACLE_VERSION_MINOR=2 \
    ORACLE_VERSION_BUILD=0.1.0 \
    ORACLE_VERSION=122010 \
    GLIBC_VERSION=2.24-r0 \
    SERVER_HTTPLOCAL=10.1.10.244:8000
    
RUN set -ex \
    && apt-get update \
    && apt-get install -y libaio1 \
    && apt-get install -y unzip \
    && apt-get install -y curl \
    && curl -o /tmp/instantclient.zip http://${SERVER_HTTPLOCAL}/instantclient-basic-linux.x64-${ORACLE_VERSION_MAJOR}.${ORACLE_VERSION_MINOR}.${ORACLE_VERSION_BUILD}.zip \
    && curl -o /tmp/instantclient-sdk.zip http://${SERVER_HTTPLOCAL}/instantclient-sdk-linux.x64-${ORACLE_VERSION_MAJOR}.${ORACLE_VERSION_MINOR}.${ORACLE_VERSION_BUILD}.zip \
    && mkdir -p opt/oracle \
    && unzip /tmp/instantclient.zip -d /opt/oracle \
    && unzip /tmp/instantclient-sdk.zip -d /opt/oracle \
    && ln -s /opt/oracle/instantclient_12_2/libclntsh.so.12.1 /opt/oracle/instantclient_12_2/libclntsh.so \
    && ln -s /opt/oracle/instantclient_12_2/libocci.so.12.2 /opt/oracle/instantclient_12_2/libocci.so \
    && rm -f /tmp/instantclient*.zip \
    && apt-get autoremove -y \
    && apt-get clean && apt-get autoclean \
    && rm -rf /tmp/* /var/tmp/* \
    && rm -rf /var/lib/apt/lists/* \
    && rm -f /var/cache/apt/archives/*.deb /var/cache/apt/archives/partial/*.deb /var/cache/apt/*.bin

ENV LD_LIBRARY_PATH=/lib:/usr/lib:/usr/glibc-compat/lib:/opt/oracle/instantclient_12_2
ENV OCI_HOME=/opt/oracle/instantclient_12_2
ENV OCI_LIB_DIR=/opt/oracle/instantclient_12_2
ENV OCI_INCLUDE_DIR=/opt/oracle/instantclient_12_2/sdk/include
ENV OCI_VERSION=12

RUN echo '/opt/oracle/instantclient_12_2/' | tee -a /etc/ld.so.conf.d/oracle_instant_client.conf \
    && ldconfig

CMD [ "node" ]
