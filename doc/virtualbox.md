    VBoxManage list extpacks
    VBoxManage list vms
    VBoxManage list runningvms

    VBoxManage unregistervm $VM_NAME --delete

    VBoxManage import virtual-machine.ova --vsys 0 --vmname $VM_NAME
    
## Start and Stop    
    VBoxHeadless --startvm $VM_NAME
    
    VBoxManage startvm $VM_NAME --type headless     //gui|sdl|headless
    
    VBoxManage controlvm $VM_NAME poweroff

# Network

Get the ip address of a running vm:

    VBoxManage guestproperty get $VM_NAME "/VirtualBox/GuestInfo/Net/$ADAPTER_INDEX_STARTING_FROM_0/V4/IP"

## Network Bridge 
    VBoxManage modifyvm $VM_NAME --nic1 bridged --bridgeadapter1 ${HOST_IF_NAME} --nictype1 82545EM
    
## Network Nat
ssh:

    VBoxManage modifyvm $VM_NAME --nic1 nat --natpf1 "guestssh,tcp,127.0.0.1,2222,,22"
http:

    VBoxManage modifyvm $VM_NAME --nic1 nat --natpf1 "guesthttps,tcp,127.0.0.1,4443,,443"
    VBoxManage modifyvm $VM_NAME --nic1 nat --natpf1 "guesthttps,tcp,127.0.0.1,8080,,80"
    
remove nic

    VBoxManage modifyvm $VM_NAME --nic1 none
    
remove nat rule
    
    VBoxManage modifyvm $VM_NAME --natpf1 delete "guesthttp" 
