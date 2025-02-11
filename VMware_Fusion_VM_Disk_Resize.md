# VMware Fusion VM Disk Resize

Shutdown the VM.

Go to Hard Disk (NVME) Settings and increase the size.

You should get a message saying “Virtual disk resized successfully. Use the disk maintenance tools in your guest operating system to resize or create partitions to fill the available space.”

Start the VM.

If asked if you moved or copied the VM, choose “I moved it”.

sudo fdisk -l returns:

    …

    Disk /dev/nvme0n1: 30 GiB, 32212254720 bytes, 62914560 sectors
    Disk model: VMware Virtual NVMe Disk
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disklabel type: gpt
    Disk identifier: EA8674C6-75A3-4E7E-A8AA-B7C9595D5F65

    Device           Start      End  Sectors  Size Type
    /dev/nvme0n1p1    2048  1953791  1951744  953M EFI System
    /dev/nvme0n1p2 1953792 41940991 39987200 19.1G Linux filesystem

    …

This confirms that nvme0n1 is 30GB and that nvme0n1p2 needs to be resized.

    $ sudo growpart /dev/nvme0n1 2
    CHANGED: partition=2 start=1953792 old: size=39987200 end=41940991 new: size=60960735 end=62914526

    $sudo resize2fs /dev/nvme0n1p2
    resize2fs 1.47.0 (5-Feb-2023)
    Filesystem at /dev/nvme0n1p2 is mounted on /; on-line resizing required
    old_desc_blocks = 3, new_desc_blocks = 4
    The filesystem on /dev/nvme0n1p2 is now 7620091 (4k) blocks long.

    $df -h
    Filesystem      Size  Used Avail Use% Mounted on
    tmpfs           391M  1.7M  389M   1% /run
    /dev/nvme0n1p2   29G   17G   11G  63% /
    tmpfs           2.0G  4.0K  2.0G   1% /dev/shm
    tmpfs           5.0M  8.0K  5.0M   1% /run/lock
    efivarfs        256K   32K  225K  13% /sys/firmware/efi/efivars
    /dev/nvme0n1p1  952M  6.4M  945M   1% /boot/efi
    tmpfs           391M  124K  391M   1% /run/user/1000
