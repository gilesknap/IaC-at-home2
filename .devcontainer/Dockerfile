FROM mcr.microsoft.com/devcontainers/python:1-3.12-bullseye

# Useful tools
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
    iputils-ping \
    net-tools \
    dnsutils \
    vim \
    sshpass \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Install ansible python packages
RUN pip install \
    ansible \
    argcomplete \
    ansible-lint \
    kubernetes

# opinionated settings
RUN sed -i 's/^ZSH_THEME=.*/ZSH_THEME="dst"/' ~/.zshrc
