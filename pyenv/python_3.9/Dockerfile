### ARG syntax is expecting an argument which is referred in other image
ARG PYTHON_VERSION="3.9.0"

### FROM clause tries to find a local Docker image with that name to build a previous environment, if not, Docker will pull it from DockerHub site if it exists
FROM pyenv:latest

# Create 'python' group
RUN groupadd python
# Add 'node' group to other user
RUN useradd -m --no-log-init -r -g python ${PYTHON_USER}

### ENV syntax sets a variable value inside the image build
ENV SHARED_DIR /shared
### WORKDIR syntax changes current directory to the specified
WORKDIR ${SHARED_DIR}
RUN chown -R ${PYTHON_USER} /home/${PYTHON_USER}
RUN chown -R ${PYTHON_USER} ${SHARED_DIR}
### USER syntax changes current user to the specified
USER ${PYTHON_USER}
### EXPOSE syntax opens the specified port access
EXPOSE 8080
### ENTRYPOINT syntax allows to specified defaults for the executing container avoiding executable commands
ENTRYPOINT ["/bin/bash", "-lc"]
