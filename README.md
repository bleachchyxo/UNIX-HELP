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
  
