### FROM clause tries to find a local Docker image with that name to build a previous environment, if not, Docker will pull it from DockerHub site if it exists
FROM ubuntu:18.04

# NODE user to create
ARG NODE_USER=node
ENV NODE_USER=${NODE_USER}

# Install recommended
ENV DEBIAN_FRONTEND=noninteractive
### RUN syntax execute following bash command
RUN apt update \
    && apt install -y \
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
# Allow 'node' in RUN commands
SHELL ["/bin/bash", "-l", "-c"]

# Default Node version
ONBUILD ARG NODE_VERSION

# Default NPM version
ONBUILD ARG NPM_VERSION

# Default YARN version
ONBUILD ARG YARN_VERSION

# Run if NODE_VERSION is defined as ARG before the FROM line
ONBUILD RUN if [ ! -z ${NODE_VERSION} ]; then \
              echo "== Installing Node ${NODE_VERSION} ==" \
              && curl -sL https://deb.nodesource.com/setup_${NODE_VERSION}.x | bash - \
              && apt install -y nodejs \
              && ln -s /usr/bin/nodejs /usr/local/bin/node \
              && echo "== Installed Node ${NODE_VERSION} =="; \
            fi

# Run if NPM_VERSION is defined as ARG before the FROM line
ONBUILD RUN if [ ! -z ${NPM_VERSION} ]; then \
              echo "== Installing NPM ${NPM_VERSION} ==" \
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
