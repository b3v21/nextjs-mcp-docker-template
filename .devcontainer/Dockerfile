FROM node:24

# Install pnpm globally
RUN npm install -g pnpm

RUN apt update

RUN apt -y install postgresql \
    ripgrep \
    git \
    fd-find

WORKDIR /home/node/work

COPY . .

# Use the node user that comes with the image
USER node