FROM node:8

# Update apt-get sources
RUN apt-get update --yes

# Install build tools
RUN apt-get install --yes build-essential wget \
	&& apt-get -y autoclean

# Install and configure pm2
RUN npm install pm2 -g
COPY process.json /process.json

# Release vars
ENV REST_RELEASE_URL https://github.com/Bitcoin-com/rest.bitcoin.com/archive/1.6.0.tar.gz
ENV REST_SHA256 746d102412af35d71b1e7dc98776d6032a72c8b80ffe8acd619224e2d10983c1

# RUN cd /tmp; wget -qO rest.tar.gz $REST_RELEASE_URL
RUN set -ex \
	&& cd /tmp \
	&& wget -qO rest.tar.gz "$REST_RELEASE_URL" \
	&& echo "$REST_SHA256 rest.tar.gz" | sha256sum -c - \
	&& mkdir /app \
	&& tar -xzvf rest.tar.gz -C /app --strip-components=1 \
	&& rm -rf /tmp/*

# Install app dependencies
RUN cd /app; npm install

# Expose ports
EXPOSE  5000

CMD ["pm2-runtime", "start", "/process.json"]
