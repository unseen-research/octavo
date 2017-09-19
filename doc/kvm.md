# Create image

    > qemu-img create -f raw example-vm-swap.img 1G

# Import image

    > virt-install --name $vmName --ram 4096 --vcpus 4 --os-type=linux --disk  $imagePath,device=disk,bus=ide  --vnc --noautoconsole --import

# Remove

    > virsh undefine $vmName

# Start, Stop, Power-off

Power off

    virsh destroy vmname

Shutdown

    > virsh shutdown vmname --mode acpi

# Edit Config

    > virsh edit <guest>

# Nat

## Host

The *default* network should be active:

    > virsh net-list --all

Bridge in device (virbr0) should be available:

    > brctl show

Ip forwarding should be enabled

    > cat /proc/sys/net/ipv4/ip_forward
    1

Otherwise enable if

    #/etc/sysctl.conf
    net.ipv4.ip_forward = 1

# Linked Clone Proxmox

A template machine contains an image named base-xxx like so:

    virtio0: local:140/base-140-disk-1.qcow2,size=32G

The linked clone machine contains a reference to that image like so:

    virtio0: local:140/base-140-disk-1.qcow2/137/vm-137-disk-1.qcow2,size=32G

In order to see all base images and their clones just use grep on the vm config files:

    > grep -r base- /etc/pve/nodes/qualle/qemu-server
    137.conf:virtio0: local:140/base-140-disk-1.qcow2/137/vm-137-disk-1.qcow2,size=32G
    140.conf:virtio0: local:140/base-140-disk-1.qcow2,size=32G

Where the vm 140 is the base vm and 137 is the linked clone vm.
