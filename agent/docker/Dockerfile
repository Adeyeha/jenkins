FROM jenkins/agent:latest-jdk17

LABEL maintainer="yemi.fagade@gmail.com"

# Install Docker CLI
USER root

# Install necessary packages and Docker CLI
RUN apt-get update && \
    apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
    echo "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list && \
    apt-get update && \
    apt-get install -y sudo && \
    apt-get install -y docker-ce-cli && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*


# Create Docker group and add Jenkins user to it
RUN groupadd docker && \
    usermod -aG docker jenkins

# Switch back to the jenkins user
USER jenkins

# Optional: Define the Docker host if needed (for connecting to Docker daemon)
# ENV DOCKER_HOST=tcp://docker:2375