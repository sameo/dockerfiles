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
RUN dnf install -y cc-oci-runtime linux-container docker-engine-1.12.1 procps vim

# Have Docker run with Clear Containers as the default runtime
RUN echo -e "#!/bin/bash\ndockerd --add-runtime cor=/usr/bin/cc-oci-runtime --default-runtime=cor --storage-driver=vfs > /dev/null 2>&1 &" > /root/start-cc.sh && chmod +x /root/start-cc.sh

ENV HOME /root
WORKDIR $HOME

# Use Clear Containers by default
CMD bash -C '/root/start-cc.sh';'bash'
