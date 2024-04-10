FROM ubuntu:latest

# Update packages and install JDK
RUN apt-get update -y && \
    apt-get install wget -y && \
    apt-get install -y default-jdk && \
    apt-get clean

# Download and extract Tomcat
RUN wget -q https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.100/bin/apache-tomcat-8.5.100.tar.gz -O /tmp/apache-tomcat-8.5.100.tar.gz && \
    tar -xvf /tmp/apache-tomcat-8.5.100.tar.gz -C /opt && \
    mv /opt/apache-tomcat-8.5.100 /opt/tomcat && \
    rm /tmp/apache-tomcat-8.5.100.tar.gz

# Download Jenkins WAR file and deploy to Tomcat
RUN wget -O /opt/tomcat/webapps/jenkins.war https://get.jenkins.io/war-stable/2.440.2/jenkins.war

# Expose port
EXPOSE 8080
