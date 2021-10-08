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
