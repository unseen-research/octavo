# Mount windows share
 
 see also [cifs manual](https://www.samba.org/samba/docs/man/manpages-3/mount.cifs.8.html)

Install required package cifs-utils:

    dnf install cifs-utils
    
Edit /etc/fstab

    //1.2.3.4/share /home/jpork/remotes/win-share cifs rw,uid=1000,gid=1000,user=win,password=winPassword,domain=winDomain,users 0 0

## Mount cifs|smb|ntfs as User

If regular users shall be able to mount set mount.cifs permissions: 

    chmod u+s /usr/sbin/mount.cifs

    
# Dns: enable short name resolution

/etc/sysconfig/network-scripts/ifcfg-$IF_NAME

    SEARCH="yourdomain.com"
    
# Dns server config

/etc/sysconfig/network-scripts/ifcfg-$IF_NAME

    PEERDNS=no
    DNS1=1.2.3.4
    
Option "PEERDNS=no". prevents /etc/resolv.conf from being modified by a DHCP server. 


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

# CentOS Text Based Installer

If graphical installer doesnt work, hit escape key directly after running CentOS installation. When the command promt appears start the linux installer in text mode by entering: 

    linux text
    