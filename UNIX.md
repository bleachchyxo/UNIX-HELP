# UNIX-HELP
Most common doubts or troubles that ocurred to me working with GNU. Mostly with Debian (Devuan).

## Profile without SUDO
Sometimes after trying using `sudo` command we get the following output:

     USER is not in the sudoers file. This incident will be reported
 
The way to fix this is going in sudo mode by typing the command:
 
     $ su
 
Once in sudo mode we going to edit the `/etc/sudoers` file by adding the desired profile into the text.
 
     # User privilege specification
     root    ALL=(ALL:ALL) ALL
 
Under the `root    ALL=(ALL:ALL) ALL` we going to add the exact same line but replacing our username instead of `root` like its shown:

     USER    ALL=(ALL:ALL) ALL

Now just save the changes in the file and your user must be sudoer already.

## Trouble updating (cdrom)
When you first install Debian/Devuan and you try to update/upgrade, most of the times it will print:

     Ign:1 cdrom://[Devuan GNU/Linux 3.1 beowulf amd64 - desktop 20210315] beowulf InRelease
     Err:2 cdrom://[Devuan GNU/Linux 3.1 beowulf amd64 - desktop 20210315] beowulf Release
      Please use apt-cdrom to make this CD-ROM recognized by APT. apt-get update cannot be used to add new CD-ROMs
     Reading package lists... Done
     E: The repository 'cdrom://[Devuan GNU/Linux 3.1 beowulf amd64 - desktop 20210315] beowulf Release' does not have a Release file.
     N: Updating from such a repository can't be done securely, and is therefore disabled by default.
     N: See apt-secure(8) manpage for repository creation and user configuration details.

When we experimenting this sort of problem it means we have some some trouble with our packages repoistory mirrors. In order to fix this we must get in the official website, package repositories. In this case `https://www.devuan.org/os/packages`. We must check for the default configurations of our mirrors, in my case `Devuan 3.1 Beowulf (oldstable)`.

     deb http://deb.devuan.org/merged beowulf          main
     deb http://deb.devuan.org/merged beowulf-updates  main
     deb http://deb.devuan.org/merged beowulf-security main

This are the given mirrors by the official website, our next move is type the following command:

     sudo nano /etc/apt/sources.list

And we should see some test like this:

     # 

     # deb cdrom:[Devuan GNU/Linux 3.1 beowulf amd64 - desktop 20210315]/ beowulf$

     deb cdrom:[Devuan GNU/Linux 3.1 beowulf amd64 - desktop 20210315]/ beowulf $

     # A network mirror was not selected during install.  The following entries
     # are provided as examples, but you should amend them as appropriate
     # for your mirror of choice.
     #
     #deb http://deb.devuan.org/merged beowulf-security main
     # deb-src http://deb.devuan.org/merged beowulf-security main

     # beowulf-updates, previously known as 'volatile'
     
     # A network mirror was not selected during install.  The following entries
     # are provided as examples, but you should amend them as appropriate
     # for your mirror of choice.
     #
     # deb http://deb.devuan.org/merged beowulf-security main
     # deb-src http://deb.devuan.org/merged beowulf-security main

First of all we must comment by adding a `#` at the start of the following line:

     deb cdrom:[Devuan GNU/Linux 3.1 beowulf amd64 - desktop 20210315]/ beowulf $

Now we must check the mirrors given in the official website and uncomment the exact same ones. If some mirror is missing, in my case:

     deb http://deb.devuan.org/merged beowulf          main

Simply add it on the file by typing it, I would recommend doing it in the given order so you avoid extra problems. Now that u added the packages repository mirrors just save the changes in the file and you are go to go. Check if its working by typing:

     $ sudo apt-get update
     $ sudo apt-get upgrade
