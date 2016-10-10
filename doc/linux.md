 Mount cifs/smb/ntfs

    chmod u+s /usr/sbin/mount.cifs

# Dns: enable short name resolution

/etc/sysconfig/network-scripts/ifcfg-$IF_NAME

    SEARCH="yourdomain.com"
    
# Dns server config

/etc/sysconfig/network-scripts/ifcfg-$IF_NAME

    PEERDNS=no
    DNS1=1.2.3.4
    
Option "PEERDNS=no". prevents /etc/resolv.conf from being modified by a DHCP server. 


# Dolphin missing icons workaround

define an environment variable

    export XDG_CURRENT_DESKTOP=kde

best place to set this var is the dolphins desktop file
  
    /usr/share/applications/org.kde.dolphin.desktop

set the exec property
    
    Exec=env XDG_CURRENT_DESKTOP=kde dolphin %u

# Remote desktop for windows

    dnf install xrdp
    
for fedora 23 its required to change the SELinux context like so:

    chcon -t bin_t /usr/sbin/xrdp /usr/sbin/xrdp-sesman    
    
# Dhcp client: use fixed dhcp-client-identifier (mac/hardware address) to register on dhcp server

add the following line to /etc/dhcp/dhclient.conf 

    send dhcp-client-identifier = hardware;

# Disable Vino Vnc Encryption For Windows Vnc Viewer

    gsettings get org.gnome.Vino require-encryption

# Java as systemd daemon (service)

## Fix libjli.so: cannot open shared object file bug

see  http://bugs.java.com/view_bug.do?bug_id=7157699

...
create a file such as this, with the path to libjli.so

    > cat /etc/ld.so.conf.d/java.conf /home/someuser/jdk1.7.0_04/jre/lib/i386/jli

This will add the the pathname to the trusted user path, that ld.so will 
use, to build its runtime cache, verify if ld.so is seeing it by doing this,
need to run it as root, and a reboot may be necessary.

    > ldconfig | grep libjli

    libjli.so -> libjli.so
...