FROM gradle:4.6.0-jdk8
MAINTAINER chkeller@gmx.net

USER root
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g --unsafe-perm @angular/cli@1.7.2