### FROM clause tries to find a local Docker image with that name to build a previous environment, if not, Docker will pull it from DockerHub site if it exists
FROM ubuntu:18.04

### ARG syntax is expecting an argument which is referred in other image
### ENV syntax sets a variable value inside the image build
# RVM version to install
ARG RVM_VERSION=stable
ENV RVM_VERSION=${RVM_VERSION}

# RMV user to create
ARG RVM_USER=docker
ENV RVM_USER=${RVM_USER}

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

# Install RVM with gpg (https://rvm.io/rvm/security)
RUN gpg --keyserver hkp://ipv4.pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
RUN echo progress-bar >> ~/.curlrc
RUN curl -sSL https://get.rvm.io | bash -s ${RVM_VERSION} --ignore-dotfiles
RUN sed -i 's/^mesg n/tty -s \&\& mesg n/g' /root/.profile
RUN echo "source /usr/local/rvm/scripts/rvm" >> /etc/bash.bashrc

### SHELL syntax starts a shell during the image build, login shell in that case
SHELL ["/bin/bash", "-l", "-c"]

# Add 'rvm' group to other user
RUN useradd -m --no-log-init -r -g rvm ${RVM_USER}

### ONBUILD syntax is execute after the the current image builds
# Set Ruby versions to install
ONBUILD ARG RVM_RUBY_VERSIONS

# Default Ruby version (first version)
ONBUILD ARG RVM_RUBY_DEFAULT

# Default Ruby version (first version)
ONBUILD ARG RVM_RAILS_VERSION

# Default Node version
ONBUILD ARG NODE_VERSION

# Default Yarn version
ONBUILD ARG YARN_VERSION

# Run if RVM_RUBY_VERSIONS is defined as ARG before the FROM line
ONBUILD RUN if [ ! -z ${RVM_RUBY_VERSIONS} ]; then \
              VERSIONS="$(echo "${RVM_RUBY_VERSIONS}" | sed -E -e 's/\s+/\n/g')" \
              &&  for i in ${VERSIONS}; do \
                    echo "== Installing RVM Ruby ${i} ==" \
                    && rvm install ${i}; \
                  done \
              && DEFAULT=${RVM_RUBY_DEFAULT:-$(echo "${VERSIONS}" | head -n1)} \
              && echo "== Setting default ${DEFAULT} ==" \
              && rvm use --default "${DEFAULT}"; \
            fi \
            && rvm cleanup all \
            && rm -rf /var/lib/apt/lists/* \
            && echo "== Installed RVM Ruby ${RVM_RUBY_DEFAULT} =="

# Run if RVM_RAILS_VERSION is defined as ARG before the FROM line
ONBUILD RUN if [ ! -z ${RVM_RAILS_VERSION} ]; then \
              echo "== Installing Rails ${RVM_RAILS_VERSION} ==" \
              && gem install rails -v ${RVM_RAILS_VERSION} \
              && gem install bundler \
              && echo "== Installed Rails ${RVM_RAILS_VERSION} with Bundler =="; \
            fi

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
