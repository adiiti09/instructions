# Installing Red Hat OpenShift Local

## Required software packages

### Debian/Ubuntu	

    sudo apt install qemu-kvm libvirt-daemon libvirt-daemon-system network-manager 

### Download binary from the below link 
https://console.redhat.com/openshift/create/local

    wget https://developers.redhat.com/content-gateway/rest/mirror/pub/openshift-v4/clients/crc/latest/crc-linux-amd64.tar.xz

Also  download or copy your pull secret. You'll be prompted for this information during installation.

### Extract the contents of the archive:

    tar xvf crc-linux-amd64.tar.xz

### Create the **~/bin** directory if it does not exist and copy the `crc` executable to it





