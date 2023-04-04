# Installing Artix Linux

First locate your disk by typing `lsblk`


    $ lsblk
    
    NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
    sda      8:0    0 223.6G  0 disk
     ├─sda1   8:1    0 222.6G  0 part /
     ├─sda2   8:2    0     1K  0 part
     └─sda5   8:5    0   975M  0 part [SWAP]
     sr0     11:0    1  1024M  0 rom
 
 In my case the disk is where I'll be installing artix is labeled as `sda` and it already has 3 partitions. We are going to proceed deleting all the partitions using `fdisk` and creating new partitions.
 
