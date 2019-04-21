FROM registry.hub.docker.com/library/centos:centos7

LABEL description="vcsim - A vCenter and ESXi API based simulator"

ENV container=docker \
    node_env=production

# Install EPEL
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 \
    && yum -y update \
    && yum -y install epel-release wget -y \
    && rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7

# Install rpms required for vcsim
RUN yum -y install golang openssl \
    && useradd go -u 8989

USER 8989

WORKDIR /home/go

RUN go get -u -v github.com/vmware/govmomi/vcsim \
    && go get -u -v github.com/vmware/govmomi/govc
RUN mkdir .tls \
    && openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout /home/go/.tls/private.key -out /home/go/.tls/cert.crt -subj "/C=US/ST=CA/L=Anytown/O=Sparkling Network/OU=IT Department/CN=vcsim.service.net"

HEALTHCHECK CMD curl -skv https://localhost:8989/about || exit 1

EXPOSE 8989

# https://go-search.org/view?id=github.com%2fvmware%2fgovmomi%2fvcsim
CMD ["/home/go/go/bin/vcsim","-httptest.serve 0.0.0.0:8989","-esx","-trace","-tls", "-tlscert", "/home/go/.tls/cert.crt", "-tlskey", "/home/go/.tls/private.key"]
