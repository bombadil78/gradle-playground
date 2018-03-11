FROM jenkins/jenkins:lts

# Only use for testing purposes
USER root
RUN apt-get update
RUN curl -fsSL https://get.docker.com/ | sh
RUN groupadd -g 985 docker-host
RUN usermod -a -G docker-host jenkins