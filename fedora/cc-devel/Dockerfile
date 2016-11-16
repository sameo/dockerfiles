#
#  Copyright (C) 2016 Intel Corporation
#
#  This program is free software; you can redistribute it and/or
#  modify it under the terms of the GNU General Public License
#  as published by the Free Software Foundation; either version 2
#  of the License, or (at your option) any later version.
#
#  This program is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
#
#  You should have received a copy of the GNU General Public License
#  along with this program; if not, write to the Free Software
#  Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301, USA.
#

FROM fedora:latest

MAINTAINER Samuel Ortiz "samuel.ortiz@intel.com"

RUN dnf update -y
RUN dnf install -y 'dnf-command(config-manager)'

# Install the Clear Containers and docker fedora repos
RUN dnf config-manager --add-repo http://download.opensuse.org/repositories/home:clearlinux:preview:clear-containers-2.0/Fedora_24
RUN dnf config-manager --add-repo https://yum.dockerproject.org/repo/testing/fedora/24

# Install repos public keys
RUN rpm --import http://download.opensuse.org/repositories/home:/clearlinux:/preview:/clear-containers-2.0/Fedora_24/repodata/repomd.xml.key
RUN rpm --import https://yum.dockerproject.org/gpg

# Install Clear Containers and the docker packages
RUN dnf install -y cc-oci-runtime linux-container docker-engine-1.12.1

# Install all development tools
RUN dnf install -y iproute
RUN dnf install -y libmnl libmnl-devel
RUN dnf install -y git make autoconf sysconftool automake libtool glib2-devel json-glib-devel libuuid-devel check-devel bats procps-ng

# Clone and create the build script
RUN mkdir /root/devlp/
RUN cd /root/devlp
RUN git clone https://github.com/01org/cc-oci-runtime.git
RUN echo "./autogen.sh --with-tests-bundle-path=/containers/ && ./configure --prefix=/usr --with-cc-kernel=/usr/share/clear-containers/vmlinux.container --with-cc-image=/usr/share/clear-containers/clear-containers.img --with-tests-rootfs-path=/containers" > /root/devlp/cc-oci-runtime/configure-cc-test && chmod +x /root/devlp/cc-oci-runtime/configure-cc-test

# Have Docker run with Clear Containers as the default runtime
RUN echo -e "#!/bin/bash\ndockerd --add-runtime cor=/usr/bin/cc-oci-runtime --default-runtime=cor --storage-driver=vfs > /dev/null 2>&1 &" > /root/start-cc.sh && chmod +x /root/start-cc.sh

# Prepare a busybox bundle for the Clear Containers tests
RUN mkdir -p /containers/rootfs
RUN docker export $(docker create busybox) | tar -C rootfs -xvf -

CMD bash -C '/root/start-cc.sh';'bash'