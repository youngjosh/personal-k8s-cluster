#Currently defunct
#Need to build my own jenkins image on ARM64 for slaves then build off them in this dockerfile

FROM joshuayoung/arm64-jenkins:base-2.235.1

USER root
#Install kubectl 1.18.0
RUN curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.18.0/bin/linux/amd64/kubectl" && \
  chmod +x ./kubectl && \
  mv ./kubectl /usr/local/bin/kubectl

#Install helm 3 version 3.3.0
RUN curl -sSL -o helm-v3.3.0-linux-amd64.tar.gz https://get.helm.sh/helm-v3.3.0-linux-amd64.tar.gz && \
  tar -zxvf helm-v3.3.0-linux-amd64.tar.gz && \
  mv linux-amd64/helm /usr/local/bin/helm

#Install docker
RUN sh ./install-docker.sh

#Return user
#USER jenkins