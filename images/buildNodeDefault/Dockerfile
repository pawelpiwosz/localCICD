FROM ubuntu:latest

RUN apt-get update \
  && apt-get install -y git openssh-server \
  && sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd \
  && mkdir -p /var/run/sshd \
  && adduser --quiet jenkins \
  && echo "jenkins:jenkins" |chpasswd \
  && mkdir /home/jenkins/.m2

COPY .ssh/authorized_keys /home/jenkins/.ssh/authorized_keys

RUN chown -R jenkins:jenkins /home/jenkins/

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]