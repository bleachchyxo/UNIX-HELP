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
