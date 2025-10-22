# Simple devcontainer for Daml development in Codespaces
FROM mcr.microsoft.com/vscode/devcontainers/base:ubuntu

ENV DEBIAN_FRONTEND=noninteractive

# Install required packages
USER root
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
     curl ca-certificates gnupg lsb-release git jq openssl xxd \
     openjdk-11-jdk openjfx \
  && rm -rf /var/lib/apt/lists/*

# Install Daml SDK (as the non-root 'vscode' user)
USER vscode
ENV HOME=/home/vscode
RUN curl -sSL https://get.daml.com/ | sh -s 2.10.2

# Ensure DAML is on PATH for interactive shells
RUN echo 'export PATH="$HOME/.daml/bin:$PATH"' >> /home/vscode/.bashrc \
  && echo 'export PATH="$HOME/.daml/bin:$PATH"' >> /home/vscode/.profile || true

# Make daml available in non-login shells
ENV PATH="/home/vscode/.daml/bin:${PATH}"

WORKDIR /workspaces
