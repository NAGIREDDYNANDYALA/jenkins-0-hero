FROM centos

RUN yum -y install openssh-server openssh-clients

RUN useradd remote_user && \
  echo 'remote_user:12345' | chpasswd && \
  mkdir /home/remote_user/.ssh && \
  chmod 700 /home/remote_user/.ssh

COPY remote-key.pub /home/remote_user/.ssh/authorized_keys

RUN chown remote_user:remote_user -R /home/remote_user/.ssh && \
    chmod 600 /home/remote_user/.ssh/authorized_keys

RUN /usr/bin/ssh-keygen -A

EXPOSE 22
RUN rm -rf /run/nologin

RUN yum -y install mysql

RUN yum update -y && \
    yum -y install python36 && \
    pip3 install awscli --upgrade --user

ENV PATH=~/.local/bin:$PATH
CMD ["/usr/sbin/sshd", "-D", "-e"]