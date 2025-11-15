FROM node:24

# Install pnpm globally
RUN npm install -g pnpm

RUN apt update

RUN apt -y install postgresql \
    postgresql-client \
    locales \
    ripgrep \
    git \
    fd-find

# allow passwordless sudo
RUN apt-get install -y sudo \
    && echo node ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/node \
    && chmod 0440 /etc/sudoers.d/node

WORKDIR /home/node/work

COPY . .

# Use the node user that comes with the image
USER node