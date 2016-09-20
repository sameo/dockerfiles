FROM fedora:latest

MAINTAINER Samuel Ortiz "samuel.ortiz@intel.com"

RUN dnf update -y
RUN dnf install -y 'dnf-command(config-manager)'
RUN dnf config-manager --add-repo http://download.opensuse.org/repositories/home:clearlinux:preview:clear-containers-2.0/Fedora_24
RUN dnf config-manager --add-repo https://yum.dockerproject.org/repo/testing/fedora/24
RUN rpm --import https://yum.dockerproject.org/gpg
RUN dnf install -y cc-oci-runtime linux-container docker-engine
RUN dnf install -y iproute
RUN dnf install -y libmnl libmnl-devel
RUN dnf install -y git make autoconf sysconftool automake libtool glib2-devel json-glib-devel libuuid-devel check-devel bats procps-ng

RUN echo "dockerd --add-runtime cor=/usr/bin/cc-oci-runtime --default-runtime=cor --storage-driver=vfs &" > /run_dockerd && chmod +x /run_dockerd
