FROM node:16
EXPOSE 8000

RUN echo "Installing dependencies..."

RUN apt-get update && \
    apt-get upgrade -y
RUN apt-get install -y git
RUN apt-get install -y build-essential
RUN apt-get install -y python
RUN apt-get install -y libvips-dev
RUN apt-get install -y fftw-dev
RUN apt-get install -y gcc
RUN apt-get install -y g++
RUN apt-get install -y make
RUN apt-get install -y libc6-dev

SHELL ["/bin/bash", "--login", "-c"]

# RUN echo "Installing Gatsby..."
# RUN npm install -g gatsby-cli

RUN echo "Setting up docker user ssh..."
RUN apt-get install -y openssh-client
RUN apt-get install -y sudo

RUN adduser --disabled-password -gecos '' docker
RUN adduser docker sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN mkdir -p /home/docker/.ssh && ln -s /run/secrets/user_ssh_key /home/docker/.ssh/id_ed25519
RUN chown -R docker:docker /home/docker/.ssh
RUN echo "    IdentityFile ~/.ssh/id_ed25519" >> /etc/ssh/ssh_config

RUN mkdir -p /usr/local/libs/
RUN chown -R docker:docker /usr/local/lib/

RUN mkdir -p /usr/projects/
RUN chown -R docker:docker /usr/projects/

WORKDIR /usr/projects

USER docker