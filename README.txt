ENV: Ubuntu 18.04, KVM

Setup ENV:

/etc/libvirt/qemu.conf --> security_driver = "none" ; user = "root" ; group = "kvm" ---> systemctl restart libvirtd

Installing Terraform libvirt Provider:

The libvirt provide will require:

libvirt 1.2.14 or newer
latest golang version
mkisofs is required to use the CloudInit feature.

$ sudo apt install golang-go 

$ export GOPATH=$HOME/go

$ go get github.com/dmacvicar/terraform-provider-libvirt
$ go install github.com/dmacvicar/terraform-provider-libvirt

You will now find the binary at $GOPATH/bin/terraform-provider-libvirt

terraform init ---> create $HOME/.terraform.d

cd $HOME/.terraform.d; mkdir plugins; cp $GOPATH/bin/terraform-provider-libvirt $HOME/.terraform.d/plugins


git clone https://github.com/adavarski/terraform-kvm-single-vm

cd terraform-kvm-single-vm

add your pub key to cloud_init.cfg and edit files for KVM specific env.
