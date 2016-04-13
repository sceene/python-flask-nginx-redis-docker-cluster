# Set the base image to Ubuntu
FROM dockerimages/ubuntu-core:14.04

# File Author / Maintainer
MAINTAINER Steven Mahana

# Update the repository and install Redis Server
RUN apt-get update && apt-get install -y redis-server supervisor

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Expose Redis port 6379
EXPOSE 6379

# Define mountable directories.
VOLUME ["/data"]

# Define working directory.
WORKDIR /data

# Run Redis Server
CMD ["/usr/bin/supervisord"]