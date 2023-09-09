FROM mambaorg/micromamba:latest

USER root

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    curl \
    git \
    gnupg \
    lsb-release \
    openssh-client \
    procps \
    sudo \
    unzip \
    wget \
    zip \
    zsh \
    && sudo rm -rf /var/lib/apt/lists/*

# Copy environment.yml (if found) to a temp location so we update the environment. Also
# copy "noop.txt" so the COPY instruction does not fail if no environment.yml exists.
COPY environment.yml* /tmp/micromamba-tmp/

RUN if [ -f "/tmp/micromamba-tmp/environment.yml" ]; then umask 002 && micromamba install -y --name base -f /tmp/micromamba-tmp/environment.yml; fi \
    && rm -rf /tmp/micromamba-tmp

RUN /opt/conda/bin/pip install --upgrade pip && \
/opt/conda/bin/pip install ipykernel

RUN /opt/conda/bin/python -m ipykernel install --user --name base --display-name "Main"
RUN micromamba clean --all --yes
ARG MAMBA_DOCKERFILE_ACTIVATE=1


# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>
