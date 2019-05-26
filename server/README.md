# Install GUI

## run upload_webgui.yml

1. edit ansible-vmware/files/host_vars/esxi.yml

2. build the container

sudo docker-compose up --build

3. execute the script

sudo docker exec -ti ansible-vmware.service bash

ansible-playbook upload_webgui.yml

4. ssh into the host and install the vib

ssh user@esxi

**[user@esxi:~]** esxcli software vib install -v /vmfs/volumes/datastore1/esxui_signed.vib

 - browse to ui

## Reference:

https://calvin.me/web-interface-for-esxi-without-vcenter/

