FROM jboss/wildfly:10.0.0.Final

ENV JBOSS_HOME     /opt/jboss/wildfly
ARG TEIID_VERSION
ENV TEIID_VERSION  ${TEIID_VERSION:-9.2.3}
ENV TEIID_HOME     $JBOSS_HOME

# Download and unzip Teiid server
RUN cd $JBOSS_HOME \
    && curl -O https://repository.jboss.org/nexus/service/local/repositories/releases/content/org/jboss/teiid/teiid/$TEIID_VERSION/teiid-$TEIID_VERSION-wildfly-dist.zip \
    && bsdtar -xf teiid-$TEIID_VERSION-wildfly-dist.zip \
    && chmod +x $JBOSS_HOME/bin/*.sh \
    && rm teiid-$TEIID_VERSION-wildfly-dist.zip

USER jboss

# Expose Teiid server  ports
EXPOSE 8080 9990 31000 35432

# Run Teiid server and bind to all interface
CMD ["/bin/sh", "-c", "$JBOSS_HOME/bin/standalone.sh -c standalone-teiid.xml -b 0.0.0.0 -bmanagement 0.0.0.0"]

