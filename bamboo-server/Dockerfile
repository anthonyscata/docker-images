# Bamboo Server
#
# VERSION               0.0.2

FROM phusion/baseimage:0.9.19
MAINTAINER H. Wüthrich "hw@5px.ch"

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Environment
ENV BAMBOO_VERSION 5.14.0.2
ENV BAMBOO_HOME /home/bamboo
ENV BAMBOO_SCHEME http

# Expose web and agent ports
EXPOSE 8085
EXPOSE 54663

# Add runit service
ADD bamboo-server.sh /etc/service/bamboo-server/run

# Make sure we get latet packages
RUN apt-get update && apt-get upgrade -y

# Install xmlstarlet
RUN apt-get install -yq xmlstarlet

# Install Java OpenJDK 8 and VCS tools
RUN apt-get install -yq python-software-properties && add-apt-repository ppa:webupd8team/java -y && apt-get update
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get install -yq oracle-java8-installer git subversion

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
