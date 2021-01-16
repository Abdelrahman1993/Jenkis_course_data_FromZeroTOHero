FROM jenkins/jenkins

USER root

RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    apt-get update -y && \
    apt-get -y install python3 && \
    python3 get-pip.py && \
    pip3 install ansible --upgrade

USER jenkins
