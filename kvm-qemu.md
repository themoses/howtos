# Using QEMU/KVM with Libvirt

I wanted to get away from Oracle Virtualbox by trying KVM for a little test Lab

## Making sure you are good to go

Please check if hardware virtualization is enabled by running

```bash
lscpu | grep Virtualization
Virtualization:      VT-x
```

If you won´t get back anything, please enable the corresponding virtualization feature for your CPU.

Next, check if you loaded the necessary kernel modules by running

```bash
lsmod | grep kvm
lsmod | grep virtio
```

If these commands return nothing, for example virtio, load the modules with the following command, so we can use para-virtualized devices.

```bash
sudo modprobe virtio virtio-net
```

To load these modules automatically, add them to /etc/modules-load.d/FILENAME with the module as it´s content

## Installing all necessary Packages

Install qemu as the kvm driver, virt-manager, virt-viewer, etc to use virsh properly. Also get ovmf to support UEFI

```bash
sudo pacman -S qemu virt-manager dmidecode bridge-utils virt-viewer ebtables dnsmasq openbsd-netcat ovmf
sudo usermod -a -G libvirt USERNAME
sudo systemctl enable libvirtd --now
```

## Downloading an ISO

We will be using an Alpine Linux for our test

```bash
curl 'http://dl-cdn.alpinelinux.org/alpine/v3.9/releases/x86_64/alpine-standard-3.9.3-x86_64.iso' --output ./alpine.iso
```

## Creating your first VM

Creating a VM can be done through the GUI (virt-manager) or CLI. To enable future scripting plans, the CLI is the goto solution here.

The official documentation tells us "Minimum requirements are --name, --ram, guest storage (--disk, --filesystem or --nodisks), and an install option."

This is not enough though, since we want a specific guest system.
To prevent performance drops, we should provide a --os-variant
Without the --network parameter a bridged interface will be created and used with the active network connection.

```bash
virt-install \
--name=testvm1 \
--ram=2048 \
--os-type=linux \
--os-variant=generic \
--disk path=/home/USERNAME/vms/testvm1/disk.img,bus=virtio,size=20 \
--vcpus=2 \
--cdrom=/home/USERNAME/Downloads/alpine-extended-3.9.3-x86_64.iso\
```

After the Domain (libvirt's name for a VM) the virt-viewer will open and you can proceed to install your VM.