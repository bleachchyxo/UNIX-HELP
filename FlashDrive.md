# Flash Drive

## Formating a USB
Formating a flash drive is a simple task but can be a little bit confusing the first time. So I'll be explaining to you how to format a flash drive
in the easy way. Fisrt of all you need to locate your flash drive "tag" by typing the command `df` or `lsblk`. In my case I'm going to be using df but
the output is basically the same.

    Filesystem     1K-blocks    Used Available Use% Mounted on
    udev             1915984       0   1915984   0% /dev
    tmpfs             386184     700    385484   1% /run
    /dev/sda1      959395920 5355384 905236136   1% /
    tmpfs               5120       4      5116   1% /run/lock
    tmpfs             972240   64132    908108   7% /dev/shm
    tmpfs            1930904       0   1930904   0% /sys/fs/cgroup
    tmpfs             386180      48    386132   1% /run/user/1000
    
Once we get displayed all the filesystems we plug the flash drive and execute the exact same command again and our flash drive must be appearing now on 
the output

    Filesystem     1K-blocks    Used Available Use% Mounted on
    udev             1915984       0   1915984   0% /dev
    tmpfs             386184     704    385480   1% /run
    /dev/sda1      959395920 5349080 905242440   1% /
    tmpfs               5120       4      5116   1% /run/lock
    tmpfs             972240   61264    910976   7% /dev/shm
    tmpfs            1930904       0   1930904   0% /sys/fs/cgroup
    tmpfs             386180      48    386132   1% /run/user/1000
    /dev/sdb1      262078944 3908704 258170240   2% /media/chuxo/DEVUAN 3_1

In my case my flash drive is recognized as `/dev/sdb1` so thats going to be the name I'll be refeering to. Now you need to umount the disk by typing:

    $ sudo umount /dev/sdb1
    
Once it finished umounting the disk you need to confirm you will be formating such a disk by typing:

    $ sudo mkfs.vfat /dev/sdb1
    
Once you've done this you are ready to go. Now by executing this command we'll proceed to format the flash drive

    $ sudo fsck /dev/sdb1

When the command finished executing you must get an output like this

    fsck from util-linux 2.33.1
    fsck.fat 4.1 (2017-01-24)
    /dev/sdb1: 0 files, 1/8189967 clusters

This means that you successfuly formated that flashd drive  
