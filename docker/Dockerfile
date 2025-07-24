FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Install Java, Git, curl, etc.
RUN apt-get update && \
    apt-get install -y openjdk-17-jdk git curl gnupg2 && \
    curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | tee \
        /usr/share/keyrings/jenkins-keyring.asc > /dev/null && \
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
        https://pkg.jenkins.io/debian-stable binary/ | tee \
        /etc/apt/sources.list.d/jenkins.list > /dev/null && \
    apt-get update && \
    apt-get install -y jenkins && \
    apt-get clean

# Setup Jenkins user and home
RUN mkdir -p /var/jenkins_home && chown -R jenkins:jenkins /var/jenkins_home
ENV JENKINS_HOME=/var/jenkins_home

VOLUME /var/jenkins_home

EXPOSE 8080

CMD ["java", "-jar", "/usr/share/jenkins/jenkins.war"]