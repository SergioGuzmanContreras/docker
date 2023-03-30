FROM fedora:latest

RUN dnf -y install openssh-server

RUN useradd test_user && \
    echo "test_user:12345" | chpasswd && \
    mkdir /home/test_user/.ssh  && \
    chmod 700 /home/test_user/.ssh 

#CREATE KEY IN SERVER LOCAL ssh-keygen -f remote-key
COPY remote-key.pub /home/test_user/.ssh/authorized_keys

RUN chown test_user:test_user -R /home/test_user && \
    chmod 400 /home/test_user/.ssh/authorized_keys

EXPOSE 22
RUN ssh-keygen -A

CMD ["/usr/sbin/sshd","-D"]