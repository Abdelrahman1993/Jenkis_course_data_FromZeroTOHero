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

CMD ["/usr/sbin/sshd", "-D"]
