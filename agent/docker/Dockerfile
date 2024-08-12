FROM jenkins/jenkins:lts

# Install Docker CLI
USER root

# Install necessary packages and Docker CLI
RUN apt-get update && \
    apt-get install -y apt-transport-https ca-certificates curl gnupg2 software-properties-common && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" && \
    apt-get update && \
    apt-get install -y docker-ce-cli

# Create Docker group and add Jenkins user to it
RUN groupadd docker && \
    usermod -aG docker jenkins

# Switch back to the jenkins user
USER jenkins

# Optional: Define the Docker host if needed (for connecting to Docker daemon)
# ENV DOCKER_HOST=tcp://docker:2375
