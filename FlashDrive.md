# Flash Drive

## Mounting a Flash Drive

We going to start by creating a folder to mount the flash drive

    $ mkdir /media/usb

Now try recognizing the flash drive using the command `lsblk`, in my case `sdb` and we can proceed
mounting the flash drive with the following command:

    $ sudo mount /dev/sdb /media/usb/
    
You can now `cd` into `/media/usb/` and see the content, when you're done just fire off:

    $ sudo umount /dev/sdb /media/usb/
