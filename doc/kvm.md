# Create image

    qemu-img create -f raw example-vm-swap.img 1G

# Import image

    virt-install --name $vmName --ram 4096 --vcpus 4 --os-type=linux --disk  $imagePath,device=disk,bus=ide  --vnc --noautoconsole --import

# Remove

    > virsh undefine $vmName

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