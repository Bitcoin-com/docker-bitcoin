FROM node:10

# Update apt-get sources
RUN apt-get update --yes

# Install build tools
RUN apt-get install --yes build-essential wget \
	&& apt-get -y autoclean

# Install and configure pm2
RUN npm install pm2 -g
COPY process.json /process.json

# Install typescript
RUN npm install typescript -g

# Clone latest rest
RUN git clone https://github.com/Bitcoin-com/rest.bitcoin.com.git /app

# Install app dependencies
RUN cd /app; npm install

# Expose ports
EXPOSE  5000

CMD ["pm2-runtime", "start", "/process.json"]
