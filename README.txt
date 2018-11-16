ENV: Ubuntu 18.04, KVM

Setup ENV:

$ systemctl stop/disable apparmor

/etc/libvirt/qemu.conf --> security_driver = "none" ; user = "root" ; group = "kvm" ---> systemctl restart libvirtd

Installing Terraform libvirt Provider:

$ sudo apt install golang-go 

$ export GOPATH=$HOME/go

$ go get github.com/dmacvicar/terraform-provider-libvirt
$ go install github.com/dmacvicar/terraform-provider-libvirt

You will now find the binary at $GOPATH/bin/terraform-provider-libvirt

$ terraform init ---> create $HOME/.terraform.d

$ cd $HOME/.terraform.d; mkdir plugins; cp $GOPATH/bin/terraform-provider-libvirt $HOME/.terraform.d/plugins

$ git clone https://github.com/adavarski/terraform-kvm-single-vm

$ cd terraform-kvm-single-vm

add your pub key to cloud_init.cfg and edit files for KVM specific env.

$ terraform init

$ terraform apply

Test:

$ virsh list
 Id    Name                           State
----------------------------------------------------
 6     u1804-terraform                running

$ virsh domifaddr u1804-terraform 
 Name       MAC address          Protocol     Address
-------------------------------------------------------------------------------
 vnet0      1a:4c:b6:61:ad:e2    ipv4         192.168.122.201/24

$ ssh ubuntu@192.168.122.201 "uname -a"
Linux ubuntu 4.15.0-38-generic #41-Ubuntu SMP Wed Oct 10 10:59:38 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
