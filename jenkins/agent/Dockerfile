FROM adoptopenjdk/openjdk8:jdk8u282-b08-debian

# Below is from default jenkins agent dockerfile https://github.com/jenkinsci/docker-agent

ARG KUBECTL_VERSION=1.19.4
ARG HELM_VERSION=3.5.2
ARG VERSION=4.6
ARG user=jenkins
ARG group=jenkins
ARG uid=1000
ARG gid=1000

RUN groupadd -g ${gid} ${group}
RUN useradd -c "Jenkins user" -d /home/${user} -u ${uid} -g ${gid} -m ${user}
LABEL Description="This is a base image, which allows connecting Jenkins agents via JNLP protocols" Vendor="Jenkins project" Version="${VERSION}"

ARG AGENT_WORKDIR=/home/${user}/agent

RUN apt-get update && apt-get install -y git-lfs && rm -rf /var/lib/apt/lists/*
RUN curl --create-dirs -fsSLo /usr/share/jenkins/agent.jar https://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/${VERSION}/remoting-${VERSION}.jar \
  && chmod 755 /usr/share/jenkins \
  && chmod 644 /usr/share/jenkins/agent.jar \
  && ln -sf /usr/share/jenkins/agent.jar /usr/share/jenkins/slave.jar

USER ${user}
ENV AGENT_WORKDIR=${AGENT_WORKDIR}
RUN mkdir /home/${user}/.jenkins && mkdir -p ${AGENT_WORKDIR}

VOLUME /home/${user}/.jenkins
VOLUME ${AGENT_WORKDIR}
WORKDIR /home/${user}

# From docker inbound agent https://github.com/jenkinsci/docker-inbound-agent/
USER root

COPY jenkins-agent /usr/local/bin/jenkins-agent
RUN chmod +x /usr/local/bin/jenkins-agent &&\
    ln -s /usr/local/bin/jenkins-agent /usr/local/bin/jenkins-slave

# My additions

# Install Docker
RUN apt-get update -qq \
  && apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common -y && \
  curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository \
  "deb [arch=arm64] https://download.docker.com/linux/debian \
  $(lsb_release -cs) \
  stable"
RUN apt-get update && \
  apt-get install docker-ce docker-ce-cli containerd.io -y
RUN usermod -aG docker ${user}

RUN service docker restart

#Install kubectl
RUN curl -LO "https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl" && \
  chmod +x ./kubectl && \
  mv ./kubectl /usr/local/bin/kubectl

#Install helm 3
RUN curl -sSL -o helm-v${HELM_VERSION}-linux-arm64.tar.gz https://get.helm.sh/helm-v${HELM_VERSION}-linux-arm64.tar.gz && \
  tar -zxvf helm-v${HELM_VERSION}-linux-arm64.tar.gz && \
  mv linux-arm64/helm /usr/local/bin/helm

USER ${user}

ENTRYPOINT ["/usr/local/bin/jenkins-agent"]