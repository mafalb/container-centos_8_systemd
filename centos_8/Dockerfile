FROM centos:8
ENV container docker
STOPSIGNAL SIGRTMIN+3

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN yum makecache fast && yum install -y python sudo which yum-plugin-ovl && sed -i 's/plugins=0/plugins=1/g' /etc/yum.conf

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/lib/systemd/systemd"]
