FROM container-registry.oracle.com/middleware/weblogic:12.2.1.2-dev

ARG ADMIN_PASSWORD
ARG ADMIN_USERNAME
ARG ADMIN_NAME
ARG DOMAIN_NAME
ARG ADMIN_PORT

ENV DOMAIN_NAME="${DOMAIN_NAME:-base_domain}" \
    DOMAIN_HOME=/u01/oracle/user_projects/domains/${DOMAIN_NAME:-base_domain} \
    ADMIN_NAME="${ADMIN_NAME:-AdminServer}" \
    ADMIN_USERNAME="${ADMIN_USERNAME:-weblogic}" \
    ADMIN_PORT="${ADMIN_PORT:-7001}" \
    PRODUCTION_MODE="${PRODUCTION_MODE:-prod}" \
    PATH=$PATH:/u01/oracle/oracle_common/common/bin:/u01/oracle/wlserver/common/bin:/u01/oracle/user_projects/domains/${DOMAIN_NAME:-base_domain}/bin:/u01/oracle

# Add files required to build this image
USER oracle
COPY container-scripts/* /u01/oracle/

# Configuration of WLS Domain
RUN wlst.sh -skipWLSModuleScanning /u01/oracle/create-wls-domain.py && \
    mkdir -p /u01/oracle/user_projects/domains/$DOMAIN_NAME/servers/AdminServer/security && \
    echo "username=$ADMIN_USERNAME" > /u01/oracle/user_projects/domains/$DOMAIN_NAME/servers/AdminServer/security/boot.properties && \
    echo "password=$ADMIN_PASSWORD" >> /u01/oracle/user_projects/domains/$DOMAIN_NAME/servers/AdminServer/security/boot.properties && \
    echo ". /u01/oracle/user_projects/domains/$DOMAIN_NAME/bin/setDomainEnv.sh" >> /u01/oracle/.bashrc 

EXPOSE $ADMIN_PORT

WORKDIR $DOMAIN_HOME

CMD ["/u01/oracle/createAndStartEmptyDomain.sh"] 