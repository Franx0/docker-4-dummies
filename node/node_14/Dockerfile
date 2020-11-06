### ARG syntax is expecting an argument which is referred in other image
ARG NODE_VERSION="14"
#ARG NPM_VERSION="latest"  (OPTIONAL)
#ARG YARN_VERSION="stable" (OPTIONAL)

### FROM clause tries to find a local Docker image with that name to build a previous environment, if not, Docker will pull it from DockerHub site if it exists
FROM node:latest

# Create 'node' group
RUN groupadd node
# Add 'node' group to other user
RUN useradd -m --no-log-init -r -g node ${NODE_USER}

### ENV syntax sets a variable value inside the image build
ENV SHARED_DIR /shared
### WORKDIR syntax changes current directory to the specified
WORKDIR ${SHARED_DIR}
RUN chown -R ${NODE_USER} ${SHARED_DIR}
### USER syntax changes current user to the specified
USER ${NODE_USER}
### EXPOSE syntax opens the specified port access
EXPOSE 3000
### ENTRYPOINT syntax allows to specified defaults for the executing container avoiding executable commands
ENTRYPOINT ["/bin/bash", "-lc"]
