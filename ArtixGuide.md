# Installing Artix Linux

## Partitioning the disk
First locate your disk by typing `lsblk`


    $ lsblk
    
    NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
    sda      8:0    0 223.6G  0 disk
     ├─sdb1   8:1    0 222.6G  0 part /
     ├─sdb2   8:2    0     1K  0 part
     └─sdb5   8:5    0   975M  0 part [SWAP]
     sr0     11:0    1  1024M  0 rom
 
In my case the disk is where I'll be installing artix is labeled as `sdb` and it already has 3 partitions. We are going to start by deleting all the partitions using `fdisk` and creating new partitions. The first partition must be at least `+1G`, the second partition must be at least `+30G` and the last partition will be using the rest of the disk.

To be able to use these partitions we are going to convert them into `ext4` by running the next command on every partition:

    mkfs.ext4 /dev/sdbX

## Mounting directories on the partitons

Once our partitons are ready to be used we going to proceed mounting directories on the partitions

    mount /dev/sdb2 /mnt
    mkdir /mnt/home
    mkdir /mnt/boot
    mount /dev/sdb1 /mnt/boot
    mount /dev/sdb3 /mnt/home
    
Now we can check if we did everything correct by running `lsblk` and having an output similar to this

    $ lsblk
    
    NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
     sda      8:0    0 223.6G  0 disk
     ├─sdb1   8:1    0     1G  0 part /mnt/boot
     ├─sdb2   8:2    0    30G  0 part /mnt
     └─sdb3   8:5    0 192.6G  0 part /mnt/home
     sr0     11:0    1  1024M  0 rom
    
## Installing the basics on the system

In order to install basic programs on our operative system we are going to run

    basestrap /mnt base base-devel runit elogind-runit linux linux-firmware neovim
