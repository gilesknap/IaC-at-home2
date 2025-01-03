FROM mcr.microsoft.com/devcontainers/python:1-3.12-bullseye

# We are root in a rootless container so don't warn us about this pip
ENV PIP_ROOT_USER_ACTION=ignore

# Install ansible python packages
RUN pip install \
    ansible \
    argcomplete \
    ansible-lint \
    jmespath \
    kubernetes
