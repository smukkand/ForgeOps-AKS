FROM smukkand.azurecr.io/forgerock-am:v2

# BEGIN tools for testing if the ds-idrepo is configured before AM starts.
# Installs ldap utils for querying the repo.
#USER root

# For debian
#RUN apt-get update && apt-get install ldap-utils
# Alpine:

# RUN apk add openldap-clients

USER forgerock

# We now use path based routing - so AM must be deployed on /am
#RUN mv /usr/local/tomcat/webapps/ROOT /usr/local/tomcat/webapps/am


COPY --chown=forgerock:root openam /home/forgerock/openam

#CMD ["catalina.sh", "run"]

ENTRYPOINT ["/home/forgerock/openam/boot.sh"]
