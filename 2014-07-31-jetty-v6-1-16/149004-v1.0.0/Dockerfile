FROM curlimages/curl:latest as jdk
LABEL maintainer="SAMATE, NIST"
WORKDIR /tmp
ARG ORACLE_AUTH_PARAM=''
RUN curl -L "https://download.oracle.com/otn/java/jdk/1.5.0_22/jdk-1_5_0_22-linux-amd64.bin?AuthParam=${ORACLE_AUTH_PARAM}" --output /tmp/jdk.bin

FROM ubuntu:20.04
LABEL maintainer="SAMATE, NIST"
RUN apt-get -y update && apt-get -y install --no-install-recommends curl make unzip ca-certificates
RUN curl -L "https://repo.maven.apache.org/maven2/org/apache/maven/apache-maven/3.1.1/apache-maven-3.1.1-bin.tar.gz" | tar -xzC /opt
WORKDIR /usr/lib/jvm
COPY --from=jdk /tmp/jdk.bin /tmp/jdk.bin
RUN chmod u+x /tmp/jdk.bin
RUN echo "yes" | /tmp/jdk.bin
ENV M2_HOME="/opt/apache-maven-3.1.1"
ENV JAVA_HOME="/usr/lib/jvm/jdk1.5.0_22"
ENV PATH="${PATH}:${JAVA_HOME}/bin:${M2_HOME}/bin"
WORKDIR /sard
COPY . .
