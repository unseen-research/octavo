# Load NBD Kernel module

Without options (configure with modprobe config file in /etc/modprobe.d/):

    modprobe nbd

With proper option in order to generate partition devices:

    modprobe nbd nbds_max=32 max_part=32

# Configure NBD Partition Device Generation

In order to create partition device files from the disk its required to configure the nbd kernel module properly.

Create a module configuration file in /etc/modprobe.d like

    > vim /etc/modprobe.d/custom_nbd.conf

with the following content

    options nbd nbds_max=32 max_part=32

load the nbd kernel module

    > modprobe nbd

# Generate device and partition devices (if configured)

    > qemu-nbd --connect /dev/nbd0 /path/to/image.qcow2

Inspect the device with fdisk

    fdisk -l /dev/nbd0

If nbd kernel module is configured properly you the partition devices are generted as well:

    /dev/nbd0          #disk device
    /dev/nbd0p1        #partition 1 on disk nbd0
    /dev/nbd0p2        #partition 2 on disk nbd0
