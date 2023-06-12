FROM centos:7
ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]


# Install Pacakage with Root
RUN curl -O https://download.oracle.com/java/17/archive/jdk-17_linux-x64_bin.rpm
RUN yum update -y \
    && yum install -y centos-release-scl libaio gdb \
    && yum localinstall -y jdk-17_linux-x64_bin.rpm


RUN useradd -m dev

WORKDIR /home/dev

COPY src/ /home/dev


ENV SOME_HOME=/home/dev \
    SOME_PORT=88 \
    SOME_LIB=/home/dev/lib







