FROM centos:7

RUN yum -y install openssh-server

RUN useradd remote_user && \
    echo "1234" | passwd remote_user --stdin

RUN mkdir -p /home/remote_user/.ssh && \
    chmod -R 700 /home/remote_user/.ssh && \
    chown -R remote_user:remote_user /home/remote_user

COPY remote_key.pub /home/remote_user/.ssh/authorized_keys

RUN chmod 600 /home/remote_user/.ssh/authorized_keys && \
    chown remote_user:remote_user /home/remote_user/.ssh/authorized_keys

RUN ssh-keygen -A

RUN yum -y install mysql

RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    yum update -y && \
    yum -y install python3 && \
    python3 get-pip.py && \
    pip3 install awscli --upgrade

#install docker
#RUN yum update
#RUN yum -y install \
#    apt-transport-https \
#    ca-certificates \
#    curl \
#    gnupg-agent \
 #   software-properties-common
#
#RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
#RUN add-apt-repository \
  # "deb [arch=amd64] https://download.docker.com/linux/debian \
  # $(lsb_release -cs) \
 #  stable"
#RUN yum update
#RUN yum -y install docker-ce

RUN yum install -y yum-utils
RUN yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

RUN yum install -y docker-ce
#install docker-compose

RUN  curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && \
     chmod +x /usr/local/bin/docker-compose

RUN usermod -aG docker remote_user

#####end of install docker and compose



CMD ["/usr/sbin/sshd", "-D"]
