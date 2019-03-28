FROM node:8
MAINTAINER Nayan Mevada <nayanmevada@ymail.com>

# ------------------------------------------------------------------------------
# Install dependencies
RUN echo "deb [check-valid-until=no] http://archive.debian.org/debian jessie-backports main" > /etc/apt/sources.list.d/jessie-backports.list
RUN sed -i '/deb http:\/\/deb.debian.org\/debian jessie-updates main/d' /etc/apt/sources.list
RUN apt-get -o Acquire::Check-Valid-Until=false update
RUN apt-get update && apt-get -y install git curl build-essential supervisor

# ------------------------------------------------------------------------------
# Install pm2
RUN npm install nodemon -g

# ------------------------------------------------------------------------------
# Get cloud9 source and install
RUN git clone https://github.com/c9/core.git /tmp/c9
RUN mv /tmp/c9 /cloud9
RUN cd /cloud9 && scripts/install-sdk.sh

WORKDIR /cloud9

# ------------------------------------------------------------------------------
# Copy start script
# COPY start.sh /cloud9/start.sh

# ------------------------------------------------------------------------------
# Add workspace volumes
RUN mkdir /cloud9/workspace
VOLUME /cloud9/workspace

# ------------------------------------------------------------------------------
# Set default workspace dir
ENV C9_WORKSPACE /cloud9/workspace

# ------------------------------------------------------------------------------
# Expose ports.
EXPOSE 5001

# Run app
# CMD ["nodemon", "server.js -p 5001 -l 0.0.0.0 --auth admin:admin1234"]
