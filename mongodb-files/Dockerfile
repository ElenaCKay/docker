# Offical mongodb image
FROM mongo:3.4

# Update and upgrade
RUN apt-get update && apt-get upgrade -y

# Set working directory
WORKDIR /data

# Expose mongodb port
EXPOSE 27017

# Copy custom mongodb config file
COPY mongod.conf /etc/mongod.conf

