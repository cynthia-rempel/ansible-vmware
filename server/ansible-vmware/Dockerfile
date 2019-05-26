# https://blog.ukotic.net/2018/07/01/getting-started-with-ansible-and-vmware/
# https://github.com/cloudmaniac/ansible-deploy-vmware-vm
# https://docs.ansible.com/ansible/latest/plugins/inventory/vmware_vm_inventory.html
# https://github.com/veksh/ansible-esxi
FROM registry.hub.docker.com/library/centos:centos7

LABEL description="Ansible is a radically simple IT automation system."

ENV container=docker \
    node_env=production

# Install EPEL
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 \
    && yum -y update \
    && yum -y install epel-release wget -y \
    && rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7

# Install rpms required for ansible-vmware
RUN yum -y install \
        gcc \
        git \
        make \
        openssl-devel \
        python36-devel \
        python36-pip \
        unzip
    
RUN git clone --single-branch --branch v6.8.1 https://github.com/vmware/vsphere-automation-sdk-python.git \
    && cd vsphere-automation-sdk-python \
    && pip3 install --upgrade --force-reinstall -r requirements.txt --extra-index-url file:///vsphere-automation-sdk-python/lib \
    && cd / \
    && rm -rf vsphere-automation-sdk-python \
    && pip3 install ansible
#    && curl -kvO https://github.com/veksh/ansible-esxi/archive/master.zip \
#    && unzip master.zip

COPY files /
# ansible-playbook -vvv /home/ansible/ansible-vmware/vmware_create_infra.yml
# RUN    && openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout .tls/private.key -out .tls/cert.crt -subj "/C=US/ST=CA/L=Anytown/O=Sparkling Network/OU=IT Department/CN=example.com"

CMD ["init"]
# https://github.com/MindPointGroup/ansible-vmware-provisioning
