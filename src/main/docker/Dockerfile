###########################################################################
# Dockerfile - Spring Boot Application Runner
###########################################################################

# Set the base image to java17

FROM openjdk:17-oracle

# File Author / Maintainer
LABEL org.medium.image.authors="tauseef"

# Define default environment variables
ENV APP_HOME=/opt/medium/
# Name of the executable artifact
ENV ARTIFACT_NAME=awss3-*.jar
# Java debug port
ENV DEBUG_PORT=8000

# Copy all artifacts to the home directory
# In maven/ the files as specified in the <assembly> section is stored
# and need to be added manually
COPY /maven/docker-entrypoint.sh /
COPY /maven/docker-job.sh ${APP_HOME}/
COPY /maven/$ARTIFACT_NAME ${APP_HOME}/

# Give permissions
USER root
RUN chmod 755 ${APP_HOME}/docker-job.sh
RUN chmod 755 /docker-entrypoint.sh

# setting permission to 777 because tool tries to create log directories which is not possible with 755 permissions
RUN chmod -R 777 /opt/medium

# set work directory
WORKDIR /opt/medium

# Main command
USER 185
ENTRYPOINT ["/docker-entrypoint.sh"]

