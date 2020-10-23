FROM jenkinsci/blueocean

USER root
#Install kubectl 1.18.0
RUN curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.18.0/bin/linux/amd64/kubectl"
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/local/bin/kubectl

#Install helm 3 version 3.3.0
RUN curl -sSL -o helm-v3.3.0-linux-amd64.tar.gz https://get.helm.sh/helm-v3.3.0-linux-amd64.tar.gz
RUN tar -zxvf helm-v3.3.0-linux-amd64.tar.gz
RUN mv linux-amd64/helm /usr/local/bin/helm

#Return user
#USER jenkins