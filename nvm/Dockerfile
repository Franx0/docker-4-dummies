### FROM clause tries to find a local Docker image with that name to build a previous environment, if not, Docker will pull it from DockerHub site if it exists
FROM ubuntu:18.04

### ARG syntax is expecting an argument which is referred in other image
### ENV syntax sets a variable value inside the image build
# NVM version to install
ARG NVM_VERSION="0.33.11"
ENV NVM_VERSION=${NVM_VERSION}
ENV NVM_DIR=/usr/local/nvm
RUN mkdir -p ${NVM_DIR}

# NVM user to create
ARG NVM_USER=docker
ENV NVM_USER=${NVM_USER}

# Install recommended
ENV DEBIAN_FRONTEND=noninteractive
### RUN syntax execute following bash command
RUN apt update \
    && apt install -y \
       sudo \
       curl \
       git \
       gnupg2 \
       locales \
       tzdata \
    && rm -rf /var/lib/apt/lists/*

# Use en_US.UTF-8 as our locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

### SHELL syntax starts a shell during the image build, login shell in that case
SHELL ["/bin/bash", "-l", "-c"]

# Default NVM version
ONBUILD ARG NVM_VERSION

# Default Node version
ONBUILD ARG NODE_VERSION

# Default NPM version
ONBUILD ARG NPM_VERSION

# Default YARN version
ONBUILD ARG YARN_VERSION

# Run if NVM_VERSION is defined as ARG before the FROM line
ONBUILD RUN if [ ! -z ${NVM_VERSION} ]; then \
              echo "== Installing NVM ${NVM_VERSION} ==" \
              && curl --silent -o- https://raw.githubusercontent.com/creationix/nvm/v${NVM_VERSION}/install.sh | bash \
              && . "${NVM_DIR}/nvm.sh" \
              && apt-get update \
              && echo "== Installed NVM ${NVM_VERSION} =="; \
            fi

# Run if NODE_VERSION is defined as ARG before the FROM line
ONBUILD RUN if [ ! -z ${NODE_VERSION} ]; then \
              echo "== Installing Node ${NODE_VERSION} ==" \
              # && curl -sL https://deb.nodesource.com/setup_${NODE_VERSION}.x | bash - \
              # && apt install -y nodejs \
              && source ${NVM_DIR}/nvm.sh \
              && nvm install ${NODE_VERSION} \
              && nvm cache clear \
              && nvm alias default ${NODE_VERSION} \
              && nvm use default \
              && echo "== Installed Node ${NODE_VERSION} =="; \
            fi

# Run if NPM_VERSION is defined as ARG before the FROM line
ONBUILD RUN if [ ! -z ${NPM_VERSION} ]; then \
              echo "== Installing NPM ${NPM_VERSION} ==" \
              && apt-get update \
              && npm install -g npm@${NPM_VERSION} \
              && echo "== Installed NPM ${NPM_VERSION} =="; \
            fi

# Run if YARN_VERSION is defined as ARG before the FROM line
ONBUILD RUN if [ ! -z ${YARN_VERSION} ]; then \
              echo "== Installing Yarn ${YARN_VERSION} ==" \
              && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
              && echo "deb https://dl.yarnpkg.com/debian/ ${YARN_VERSION} main" | tee /etc/apt/sources.list.d/yarn.list \
              && apt-get update \
              && apt-get install yarn \
              && echo "== Installed Yarn ${YARN_VERSION} =="; \
            fi

### Load NVM on container creation
RUN echo "source ${NVM_DIR}/nvm.sh" >> /etc/bash.bashrc
