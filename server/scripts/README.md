

# Install GUI

 - download the esxui_signed.vib

**[user@workstation:~]** wget http://download3.vmware.com/software/vmw-tools/esxui/esxui_signed.vib

 - copy esxui_signed.vib to the esxi 

**[user@workstation:~]** cp esxui_signed.vib root@esxi:/tmp

 - navigate to esxi

ssh user@esxi

**[user@esxi:~]** esxcli software vib install -v /tmp/esxui_signed.vib

 - browse to ui

firefox https://esxi/ui

## Reference:

https://calvin.me/web-interface-for-esxi-without-vcenter/


https://medium.com/@jackprice/pushing-kickstarts-with-ansible-122b2cd9c1e
https://github.com/ansible/ansible/issues/35665
https://github.com/RedHatGov/ssg-el7-kickstart
https://github.com/veksh/ansible-esxi
# Harden ESXi
https://mycloudrevolution.com/en/2019/04/09/vmware-esxi-security-configuration-with-ansible/
