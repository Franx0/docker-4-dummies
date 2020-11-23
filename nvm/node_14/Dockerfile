### ARG syntax is expecting an argument which is referred in other image
ARG NVM_VERSION="0.33.11"
ARG NODE_VERSION="14.15.0"
#ARG NPM_VERSION="latest"  (OPTIONAL)
#ARG YARN_VERSION="stable" (OPTIONAL)

### FROM clause tries to find a local Docker image with that name to build a previous environment, if not, Docker will pull it from DockerHub site if it exists
FROM nvm:latest

# Create 'node' group
RUN groupadd node
# Add 'node' group to other user
RUN useradd -m --no-log-init -r -g node ${NVM_USER}

### ENV syntax sets a variable value inside the image build
ENV SHARED_DIR /shared
### WORKDIR syntax changes current directory to the specified
WORKDIR ${SHARED_DIR}
RUN chown -R ${NVM_USER} ${SHARED_DIR}
### USER syntax changes current user to the specified
USER ${NVM_USER}
### EXPOSE syntax opens the specified port access
EXPOSE 8080
### ENTRYPOINT syntax allows to specified defaults for the executing container avoiding executable commands
ENTRYPOINT ["/bin/bash", "-lc"]
