FROM openjdk:11-jre-slim

MAINTAINER Christian A. Sueiras (https://github.com/csueiras)

# required
ARG githash
ARG version

# required
LABEL githash="$githash"
LABEL version="$version"

# required verbatim by docker-maven-plugin
COPY maven /acme-runner/
WORKDIR /acme-runner

VOLUME /acme-runner/certificates

ENV JAVA_OPTS=""
ENTRYPOINT exec java -Djava.security.egd=file:/dev/./urandom $JAVA_OPTS -jar /acme-runner/artifacts/${project.artifactId}-${project.version}.jar $0 $@
