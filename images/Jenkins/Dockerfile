FROM jenkins/jenkins

ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false
ENV CASC_JENKINS_CONFIG /var/jenkins_home/casc.yaml

USER root

RUN apt-get update \
  && apt-get install -qqy \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common \
    docker.io \
  && apt-get clean

RUN usermod -aG docker jenkins

USER jenkins

COPY plugins.txt /usr/share/jenkins/plugins.txt
COPY casc.yaml /var/jenkins_home/casc.yaml

RUN jenkins-plugin-cli -f /usr/share/jenkins/plugins.txt
