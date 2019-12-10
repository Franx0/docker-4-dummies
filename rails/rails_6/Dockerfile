### ARG syntax is expecting an argument which is referred in other image
ARG RVM_RUBY_VERSIONS="2.6.2"
ARG RVM_RUBY_DEFAULT="2.6.2"
ARG RVM_RAILS_VERSION="6.0"
ARG NODE_VERSION="12"
ARG YARN_VERSION="stable"

### FROM clause tries to find a local Docker image with that name to build a previous environment, if not, Docker will pull it from DockerHub site if it exists
FROM rvm:latest

### ENV syntax sets a variable value inside the image build
ENV SHARED_DIR /shared
### WORKDIR syntax changes current directory to the specified
WORKDIR ${SHARED_DIR}
RUN chown -R ${RVM_USER} ${SHARED_DIR}
### USER syntax changes current user to the specified
USER ${RVM_USER}
### EXPOSE syntax opens the specified port access
EXPOSE 3000
### ENTRYPOINT syntax allows to specified defaults for the executing container avoiding executable commands
ENTRYPOINT ["/bin/bash", "-lc"]
