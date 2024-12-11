# Storage Managing

## Extra Storage

We can check our installed drives when running `lsblk` command

    NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
    sda      8:0    0 223.6G  0 disk
    ├─sda1   8:1    0     1G  0 part /boot
    ├─sda2   8:2    0    30G  0 part /
    └─sda3   8:3    0 192.6G  0 part /home
    sdb      8:16   0 238.5G  0 disk
    └─sdb1   8:17   0 238.5G  0 part
    sr0     11:0    1  1024M  0 rom

Our main drive is called `sda`, thats where our OS runs and currently our whole storage space. `sdb` is our second drive which at the moment can't be used since it's not mounted yet.

## Mounting a drive

### Create a mount point
Create the directory where the disk will be mounted. Typically it's done under `/mnt` but you can choose any location.

    sudo mkdir /mnt/storage
### Mounting the partition temporarily
    sudo mount /dev/sdb1 /mnt/storage
Now, you can access the extra storage at `/mnt/storage` but it will umount after rebooting your machine.

## Make the mount permanent
To ensure the partition is automatically mounted after each reboot, add an entry to the `/etc/fstab` file.
### Getting the UUID of the partition
    blkid /dev/sdb1

Should return a similar output;

    /dev/sdb1: UUID="e346c668-c89d-4f6d-ad03-9d70f7ece4cb" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="4cc32217-01"
Now edit the `/etc/fstab` adding a line at the very end of the file

    # /dev/sda1 (extra storage)
    UUID=e346c668-c89d-4f6d-ad03-9d70f7ece4cb       /mnt/storage    ext4            rw,relatime     0 2

- Replace `e346c668-c89d-4f6d-ad03-9d70f7ece4cb` with the actual UUID
- Replace `/mnt/storage` with your mount point
- Replace `ext4` with the type of filesystem you are using on the drive

### Testing the `/etc/fstab` configuration
To check if everything is set up correctly, you can test the `fstab` entry without rebooting;

    sudo mount -a
If there are no errors, the system will automatically mount the disk on boot. Now we just need to verify the mount;

    df -h
This shows all mounted filesystems, including the new storage.

 # Flash Drive

## Mounting a Flash Drive

We going to start by creating a folder to mount the flash drive

    $ mkdir /media/usb

Now try recognizing the flash drive using the command `lsblk`, in my case `sdb` and we can proceed
mounting the flash drive with the following command:

    $ sudo mount /dev/sdb /media/usb/
    
You can now `cd` into `/media/usb/` and see the content, when you're done just fire off:

    $ sudo umount /dev/sdb /media/usb/

## Formating a Flash Drive

First of all enter as a `root user`, now we can proceed formating the flash drive by using the command

    # fdisk /dev/sdb
  
Next type `d` to delete a partition, type `1` to select the 1st partition then press `enter`. Continue repeating this
process until you've deleted every partition left.


Now we need to create the new partition by typing `n`, then press `enter` 3 times to accept the default options and
now to type `w` to write the new information into the flash drive.


And finally we need to create the filesystem by typing

    # mkfs.ext4 /dev/sdb

## Burning an ISO into a flash drive

You want to get into `root user` and locate your flash drive, in my case `/dev/sdb/` and the `iso` file is called
`devuan_beowulf_3.1.1_i386_desktop.iso`

    # dd if=devuan_beowulf_3.1.1_i386_desktop.iso of=/dev/sdb status="progress"
