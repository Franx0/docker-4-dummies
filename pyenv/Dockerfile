### FROM clause tries to find a local Docker image with that name to build a previous environment, if not, Docker will pull it from DockerHub site if it exists
FROM ubuntu:18.04

### ARG syntax is expecting an argument which is referred in other image
### ENV syntax sets a variable value inside the image build

# Python user to create
ARG PYTHON_USER=docker
ENV PYTHON_USER=${PYTHON_USER}

# Install recommended
ENV DEBIAN_FRONTEND=noninteractive
### RUN syntax execute following bash command
RUN apt update \
    && apt install -y \
       build-essential libssl-dev zlib1g-dev libbz2-dev \
       libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
       xz-utils tk-dev libffi-dev liblzma-dev python-openssl \
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

# Install pyenv
ENV PYENV_ROOT=/home/${PYTHON_USER}/.pyenv
ENV PATH=/home/${PYTHON_USER}/.pyenv/bin:${PATH}
RUN curl https://pyenv.run | bash
RUN echo "export PATH=/home/${PYTHON_USER}/.pyenv/bin:${PATH}" >> /etc/bash.bashrc
RUN echo "eval $(pyenv init -)" >> /etc/bash.bashrc
RUN echo "eval $(pyenv virtualenv-init -)" >> /etc/bash.bashrc
RUN exec ${SHELL}

### SHELL syntax starts a shell during the image build, login shell in that case
SHELL ["/bin/bash", "-l", "-c"]

### ONBUILD syntax is execute after the the current image builds
# Set Python version to install
ONBUILD ARG PYTHON_VERSION

# Run if PYTHON_VERSION is defined as ARG before the FROM line
ONBUILD RUN if [ ! -z ${PYTHON_VERSION} ]; then \
              echo "== Installing Python ${PYTHON_VERSION} ==" \
              && pyenv update \
              && pyenv install ${PYTHON_VERSION} \
              && pyenv global ${PYTHON_VERSION} \
              && echo "== Installed Python ${PYTHON_VERSION} =="; \
            fi
