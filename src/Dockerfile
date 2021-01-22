# This file is part of container-centos_8_systemd
# Copyright (c) 2021 Markus Falb <markus.falb@mafalb.at>
#
# container-centos_8_systemd is free software: you can redistribute it 
# and/or modify it under the terms of the GNU General Public License as
# published by the Free Software Foundation, either version 3 of the
# License, or (at your option) any later version.
#
# container-centos_8_systemd is distributed in the hope that it will be
# useful, but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with container-centos_8_systemd.
# If not, see <https://www.gnu.org/licenses/>.

FROM centos:8
ENV container docker
STOPSIGNAL SIGRTMIN+3

ENV container docker

RUN touch /var/lib/rpm/* && yum makecache && yum --assumeyes install python3 sudo which systemd iproute

RUN if test -d /lib/systemd/system/sysinit.target.wants/ ; then (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done);\
 rm -f /lib/systemd/system/multi-user.target.wants/*;\
 rm -f /etc/systemd/system/*.wants/*;\
 rm -f /lib/systemd/system/local-fs.target.wants/*;\
 rm -f /lib/systemd/system/sockets.target.wants/*udev*;\
 rm -f /lib/systemd/system/sockets.target.wants/*initctl*;\
 rm -f /lib/systemd/system/basic.target.wants/*;\
 rm -f /lib/systemd/system/anaconda.target.wants/*;\
fi

RUN if test -d /lib/systemd/system/sysinit.target.wants/ ; then ln -s /lib/systemd/system/systemd-user-sessions.service /lib/systemd/system/multi-user.target.wants/; fi

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/lib/systemd/systemd"]
