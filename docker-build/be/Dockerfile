# Choose a base image
FROM openjdk:8u342-jdk

# Set environment variables
ENV JAVA_HOME="/usr/local/openjdk-8/"
ENV PATH="/opt/apache-doris/be/bin:$PATH"

# Download the software into the Docker image
COPY ./resource/apache-doris-2.1.3-bin.tar.gz /opt
RUN mkdir /opt/apache-doris && \
    tar -xvzf /opt/apache-doris-2.1.3-bin.tar.gz -C /opt/apache-doris --strip-components=1

WORKDIR /opt/apache-doris/be

RUN apt-get update && \
    apt-get install -y default-mysql-client && \
    apt-get clean

RUN swapoff -a

ENTRYPOINT ["/opt/apache-doris/be/bin/start_be.sh"]