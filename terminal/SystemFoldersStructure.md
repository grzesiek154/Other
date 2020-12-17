$ - ozacza to ze jestesmy zalogowanie w terminalu jako zwykly uzytkownik

![Image result for linux directories description](https://static.thegeekstuff.com/wp-content/uploads/2010/11/filesystem-structure.png)

A typical Linux system has the following directories:

=> **/** : This is the root directory.

=> **/bin** : This directory contains executable programs which are needed in single user mode and to bring the system up or repair it.

=> **/boot** : Contains static files for the boot loader. This directory only holds the files which are needed during the boot process.

=> **/dev** : Special or device files, which refer to physical devices such as hard disk, keyboard, monitor, mouse and modem etc

=> **/etc** : Contains configuration files which are local to the machine. Some larger software packages, like Apache, can have their own subdirectories below /etc i.e. /etc/httpd. Some important subdirectories in /etc:

- **/etc/skel** : When a new user account is created, files from this directory are usually copied into the userâ€™s home directory.
- **/etc/X11** : Configuration files for the X11 window system .
- **/etc/sysconfig** : Important configuration file used by SysV script stored in /etc/init.d and /etc.rcX directories
- **/etc/cron.\*** : cron daemon configuration files which is used to execute scheduled commands

=> **/home** : Your sweet home to store data and other files. However in large installation yhe structure of /home directory depends on local administration decisions.

=> **/lib** : This directory should hold those shared libraries that are necessary to boot the system and to run the commands in the root filesystem.

=> **/lib64** : 64 bit shared libraries that are necessary to boot the system and to run the commands in the root filesystem.

=> **/mnt** : This directory contains mount points for temporarily mounted filesystems

=> **/opt** : This directory should contain add-on packages such as install download firefox or static files

=> **/proc** : This is a mount point for the proc filesystem, which provides information about running processes and the kernel.

=> **/root** : This directory is usually the home directory for the root user.

=> **/sbin** : Like /bin, this directory holds commands needed to boot the system, but which are usually not executed by normal users, root / admin user specific commands goes here.

=> **/tmp** : This directory contains temporary files which may be deleted with no notice, such as by a regular job or at system boot up.

=> **/usr** : This directory is usually mounted from a separate partition. It should hold only sharable, read-only data, so that it can be mounted by various machines run ning Linux (useful for diskless client or multiuser Linux network such as university network). Programs, libraries, documentation etc. for all user-related programs.

=> **/var** : This directory contains files which may change in size, such as spool and log files.

=> **/lost+found** : Every partition has a lost+found in its upper directory. Files that were saved during failures are here, for e.g ext2/ext3 fsck recovery.