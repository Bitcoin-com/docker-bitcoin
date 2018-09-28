FROM node:8

# Update apt-get sources
RUN apt-get update --yes

# Install build tools
RUN apt-get install --yes build-essential wget git \
	&& apt-get -y autoclean

# Install and configure pm2
RUN npm install pm2 -g
COPY process.json /process.json

# Clone repo
RUN git clone https://github.com/Bitcoin-com/rest.bitcoin.com.git app
RUN cd app; git checkout wormhole-merge2

# Install app dependencies
RUN npm install

# Expose ports
EXPOSE  5000

CMD ["pm2-runtime", "start", "/process.json"]
