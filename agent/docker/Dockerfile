# FROM jenkins/agent:latest-bookworm-jdk21

# LABEL maintainer="yemi.fagade@gmail.com"

# # Install Docker CLI
# USER root

# # Install necessary packages and Docker CLI
# RUN apt-get update && \
#     apt-get install -y \
#     apt-transport-https \
#     ca-certificates \
#     curl \
#     gnupg \
#     lsb-release && \
#     curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
#     echo "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list && \
#     apt-get update && \
#     apt-get install -y sudo && \
#     apt-get install -y docker-ce-cli && \
#     apt-get clean && \
#     rm -rf /var/lib/apt/lists/*


# # Create Docker group and add Jenkins user to it
# RUN groupadd docker && \
#     usermod -aG docker jenkins


# # RUN systemctl enable docker.service
# # RUN systemctl enable containerd.service

# # RUN docker run hello-world

# # Switch back to the jenkins user
# USER jenkins

# # Optional: Define the Docker host if needed (for connecting to Docker daemon)
# # ENV DOCKER_HOST=tcp://docker:2375



FROM jenkins/agent:latest-bookworm-jdk17

LABEL maintainer="yemi.fagade@gmail.com"

# Install necessary packages
USER root

# Install packages and set up Docker repository
RUN apt-get update && \
    apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release && \
    # Create a directory for Docker’s GPG key
    mkdir -m 0755 -p /etc/apt/keyrings && \
    # Add Docker’s official GPG key
    curl -fsSL https://download.docker.com/linux/debian/gpg | tee /etc/apt/keyrings/docker.asc && \
    # Add the Docker repository to Apt sources
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
    $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null && \
    # Update Apt and install Docker packages
    apt-get update && \
    apt-get install -y \
    docker-ce \
    docker-ce-cli \
    containerd.io \
    docker-buildx-plugin \
    docker-compose-plugin && \
    # Clean up
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Run Docker Hello World to verify installation
# RUN service docker start
# RUN docker run hello-world

# Create Docker group and add Jenkins user to it
# RUN groupadd docker && \
RUN usermod -aG docker jenkins

# Switch back to the jenkins user
USER jenkins

# Optional: Define the Docker host if needed (for connecting to Docker daemon)
# ENV DOCKER_HOST=tcp://docker:2375
