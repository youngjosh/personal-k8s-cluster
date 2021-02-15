#Builds off my base Jenkins arm64 image

FROM joshuayoung/arm64-jenkins:2.263.4

#Disable setup mode
ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false

USER root

#Install Jenkins Plugins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN java -jar /usr/lib/jenkins-plugin-manager.jar -f /usr/share/jenkins/ref/plugins.txt

#JCasC
COPY jenkins-casc.yaml /usr/local/jenkins-casc.yaml
ENV CASC_JENKINS_CONFIG /usr/local/jenkins-casc.yaml

#Return user
USER jenkins