# Create image

    qemu-img create -f raw example-vm-swap.img 1G

# Import image

virt-install -n vmname -r 2048 --os-type=linux   --os-variant=Generic --disk   /var/lib/libvirt/images/18129005F1-disk1.img,device=disk,bus=virtio  --vnc --noautoconsole --import

# Start, Stop, Power-off

Power off
    
    virsh destroy vmname

Shutdown 

    virsh shutdown vmname --mode acpi
    
# Edit Config

    virsh edit <guest>
    
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