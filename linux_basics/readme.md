# Linux Basics

The Raspberry Pi 3 embedded system is quite a complex system with a lot of features and complicated hardware. While it is possible to write software that runs directly on the embedded processor (called a bare-metal application) it is way to complex. Typically an Operating System (OS) is installed to manage all the hardware and resources making it easier for software developers to create application to run on the system. That way the hardware can be accessed through services provided by the OS.

Choosing an operating system for an embedded system mainly depends on the hardware as not each operating system will provide support for the embedded system.

Some existing operating systems are shown in the image below:

![Some operating systems](img/list-of-operating-systems.jpg)

The main operating systems that have support for the Raspberry Pi 3 are:

* Raspbian, Ubuntu Mate, OSMC, OpenElec, ... (Linux based)
* Windows IoT core (Windows based)
* Risc OS (Real-time OS)

Further down the course we will focus on the Raspbian linux distribution.

> #### Note::
> While the information and examples presented here will be valid for most Linux distro's, some information and commands may only work for Debian based distro's.

## Linux kernel and Linux Distribution

Linux was originally developed as a free operating system for personal computers based on the Intel x86 architecture, but has since been ported to more computer hardware platforms than any other operating system. This includes desktop PCs, servers, mainframes, supercomputers, smartphones, tablets, TVs, embedded systems, ...

Guess what your TV decoder at home is running.

When people refer to linux, it can actually mean two different things.

First is the Linux kernel which was created in 1991 by a Finnish computer science student called Linus Torvalds. It was based on the Minix operating system. Linus made the project open source and allowed people to freely use and contribute to the Linux kernel. Currently the official kernel received contributions from over 12000 programmers.

Second, are so-called "Linux distributions", also called distros. They are complete operating systems that consist of the Linux kernel itself and many other applications and software packages. Because they typically contain a lot of software created by the GNU project, some people (mostly GNU guys themselves) claim that they should be called GNU/Linux instead of just Linux.

<!-- In 1983, Richard Stallman, founder of the Free Software Foundation, set forth plans of a complete Unix-like operating system, called GNU, composed entirely of free software. In September of that year, Stallman published a manifesto in Dr. Dobb's Journal detailing his new project publicly, outlining his vision of free software.[7][8] Software development work began in January 1984. By 1991, the GNU mid-level portions of the operating system were almost complete, and the upper level could be supplied by the X Window System, but the lower level (kernel, device drivers, system-level utilities and daemons) was still mostly lacking. The GNU kernel was called GNU Hurd. The Hurd followed an ambitious design which proved unexpectedly difficult to implement and has only been marginally usable.

Independently, in 1991, Linus Torvalds released the first version of the Linux kernel. Early Linux developers ported GNU code, including the GNU C Compiler, to the kernel. The free software community adopted the use of the Linux kernel as the missing kernel for the GNU operating system. This work filled the remaining gaps in providing a completely free operating system.

Over the next few years, several suggestions arose for naming operating systems using the Linux kernel and GNU components. In 1992, the Yggdrasil Linux distribution adopted the name "Linux/GNU/X". In Usenet and mailing-list discussions, one can find usages of "GNU/Linux" as early as 1992[9] and of "GNU+Linux" as early as 1993.[10] The Debian project, which was at one time sponsored by the Free Software Foundation, switched to calling its product "Debian GNU/Linux" in early 1994;[6][11][12][13] This change followed a request by Richard Stallman (who initially proposed "LiGNUx," but suggested "GNU/Linux" instead after hearing complaints about the awkwardness of the former term).[14] GNU's June 1994 Bulletin describes "Linux" as a "free Unix system for 386 machines" (with "many of the utilities and libraries" from GNU),[15] but the January 1995 Bulletin switched to the term "GNU/Linux" instead.[16]

Stallman's and the FSF's efforts to include "GNU" in the name started around 1994, but were reportedly mostly via private communications (such as the above-mentioned request to Debian) until 1996.[17][18] In May 1996, Stallman released Emacs 19.31 with the Autoconf system target "linux" changed to "lignux" (shortly thereafter changed to "linux-gnu" in emacs 19.32),[19][20] and included an essay "Linux and the GNU system"[21] suggesting that people use the terms "Linux-based GNU system" (or "GNU/Linux system" or "Lignux" for short). He later used "GNU/Linux" exclusively, and the essay was superseded by Stallman's 1997 essay, "Linux and the GNU project".[1] -->

When we are talking about embedded Linux we actually are talking about the same kernel code running on millions of other systems. There is no separate code base for embedded systems. When we however build a Linux system for an embedded target we do exclude features we won't be using. We are also cross-compiling the kernel to binary code that can run on the target system.

### The Linux kernel

The Linux kernel **provides the core system facilities** required for any system based upon Linux to operate correctly. It has complete control over everything that occurs in the system. Application software relies upon specific features of the Linux kernel such as its handling of hardware devices and its **provision of many fundamental abstractions** such as virtual memory, sockets, tasks (known as processes), files and many others. A diagram is shown below

![The Linux kernel and it's services](img/kernel_services.png)

The main roles of the kernel are

* Manage all the hardware resources such as CPU, memory, I/O, ...
* Provide a set of portable, architecture - and hardware independent APIs (Application Programmable Interface) to allow user space applications and libraries to use the hardware resources.
* Handle concurrent accesses and usage of hardware resources from different applications. Example: a single network interface is used by multiple user space applications through various network connections. The kernel is responsible for "multiplexing" the hardware resource.

The main interface between the kernel and user space is the set of system calls that are provided by the kernel (about 300 system calls that provide the main kernel services).

These services include:

* file and device operations
* networking operations
* inter-process communication
* process management
* memory mapping
* timers
* threads
* synchronization primitives
* ...

Some key features of the kernel are:

* Portability and hardware support: it runs on most architectures.
* Scalability: Linux can run on super computers as well as on tiny devices (4 MB of RAM is enough).
* Compliance to standards and interoperability
* Exhaustive networking support
* Security: It can't hide its ﬂaws. Its code is reviewed by many experts.
* Stability and reliability
* Modularity: Can include only what a system needs even at run time.
* Easy to program: You can learn from existing code. Many useful resources on the net.

Very important to know is that the **kernel interface is stable over time**. This basically means that only new system calls can be added by the kernel developers and no old calls can be removed. This means that applications running on an older kernel version should always work on a newer one. The system call interface is actually wrapped by the C library and user space applications usually never make a system call directly but rather use the corresponding C library functions.

## The MAN-pages

The most important command you need to know is the `man` command, which provides an interface to the reference manuals. By adding a command after the man command you can consult the man-pages for that particular command. These pages provide all the information you need to know to use the command such as general information, a detailed description of the arguments and usage examples. Let's see an example:

```shell
pi@HAL:/$ man ls
```

Which gives the output shown in the image below. We can for example see if we add "-a" after the "ls" command it will also display hidden files (In Linux hidden files start with a dot, for example ".ssh"). You can scroll through the man-pages using the arrow keys.

![Output of "man ls" command](img/man_pages_ls.png)

Searching the current man-page can be done by first typing a slash ("/"), followed by your search term. Jumping to the next hit can be done by hitting the "n" key, while jumping back is done with "SHIFT-n".

Exiting the man-pages is achieved by hitting the "q" key.

> #### Assignment::The cat command
>
> What does the `cat` command do? How can it be used to output the content of a file? Try to read the file "/proc/cpuinfo"

<!-- How to place a break here? -->

> #### Assignment::The dmesg command
>
> What does the `dmesg` command do?

<!-- How to place a break here? -->

> #### Assignment::The free command
>
> The `free` command shows the system memory usage. How can you make the numbers "human readable"?


## The Linux Filesystem

Based on [Digital Ocean - How To Understand the Filesystem Layout in a Linux VPS](https://www.digitalocean.com/community/tutorials/how-to-understand-the-filesystem-layout-in-a-linux-vps)

### Some brief notes on the History of the Linux Filesystem Layout

Linux inherits many of its concepts of filesystem organization from its Unix predecessors. As far back as 1979, Unix was establishing standards to control how compliant systems would organize their files.

The Linux File system Hierarchy Standard (checkout [Filesystem Hierarchy Standard](http://www.pathname.com/fhs/)), or FHS for short, is a prescriptive standard maintained by the Linux Foundation that establishes the organizational layout that Linux distributions should uphold for interoperability, ease of administration, and the ability to implement cross-distro applications reliably.

One important thing to mention when dealing with these systems is that Linux implements just about **everything as a file**. This means that a text file is a file, a directory is a file (simply a list of other files), a printer is represented by a file (the device drivers can send anything written to the printer file to the physical printer), a serial port is a file, etc.

Although this is in some cases an oversimplification, it informs us of the approach that the designers of the system encouraged: passing text and bytes back and forth and being able to apply similar strategies for editing and accessing diverse components.

### Traversing the Filesystem

Before actually delving into the file system layout, you need to know a few basics about how to navigate a file system from the command line. We will cover the bare minimum here to get you on your feet.

The first thing you need to do is orient yourself in the filesystem. There are a few ways to do this, but one of the most basic is with the `pwd` command, which stands for "print working directory":

```shell
pi@HAL:/$ pwd
/home/pi
```

This simply returns the directory you are currently located in.

To see what files are in the current directory, you can issue the `ls` command, which stands for "list":

```shell
pi@HAL:/$ ls
bin   dev  home  lost+found  mnt  proc  run   selinux  sys  usr
boot  etc  lib   media       opt  root  sbin  srv      tmp  var
```

This will give an overview of all directories and files in your current directory.

The `ls` command can take some optional flags. Flags modify the commands default behavior to either process or display the data in a different way.

The two most common flags are probable `-l` and `-a`. The first flag forces the command to output information in long-form:

```shell
pi@HAL:/$ ls -l
total 88
drwxr-xr-x  2 root root  4096 Jun 20 10:55 bin
drwxr-xr-x  2 root root 16384 Jan  1  1970 boot
drwxr-xr-x 12 root root  3060 Sep 24 13:31 dev
drwxr-xr-x 99 root root  4096 Sep 24 13:31 etc
drwxr-xr-x  3 root root  4096 Jun 20 07:48 home
drwxr-xr-x 12 root root  4096 Jun 20 10:42 lib
-rw-r--r--  1 root root     0 Sep 24 13:37 log.txt
drwx------  2 root root 16384 Jun 20 07:34 lost+found
drwxr-xr-x  2 root root  4096 Jun 20 07:36 media
...
```

This produces output with one line for each file or directory (the name is on the far right). This has a lot of information that we are not interested in right now. One part we are interested in though is the very **first character**, which tells us what **kind of file** it is. The three most common types are:
* `-`: Regular file
* `d`: Directory (a file of a specific format that lists other files)
* `l`: A hard or soft link (basically a shortcut to another file on the system)

The `-a` flag lists all files, including hidden files. In Linux, files are hidden automatically if they begin with a dot:

```shell
pi@HAL:/$ ls -a
.   bin   dev  home  log.txt     media  opt   root  sbin     srv  tmp  var
..  boot  etc  lib   lost+found  mnt    proc  run   selinux  sys  usr
```

The first two entries, `.` and `..` are special. The `.` directory is a shortcut that means "the current directory". The `..` directory is a shortcut that means "the current directory's parent directory".

Now that you can find out where you are in the file system and see what is around you, it is time to learn how to move throughout the file system.

To change to a different directory, you issue the `cd` command, which stands for "change directory":

```shell
pi@HAL:/$ cd /home
pi@HAL:/home$
```

You can follow the command with either an absolute or a relative pathname.

* An **absolute path** is a file path that specifies the location of a directory from at the top of the directory tree. Absolute paths begin with a "/", as you see above.
* A **relative path** is a file path that is relative to the current working directory. This means that instead of defining a location from the top of the directory structure, it defines the location in relation to where you currently are.

For instance, if you want to move to the home directory of the pi user, while in the directory `/home`, you can issue the command:

```shell
pi@HAL:/home$ cd pi
pi@HAL:/home/pi$
```

The lack of the `/` from the beginning tells to use the current directory as the base for looking for the path.

This is where the `..` directory link comes in handy. To move to the parent directory of your current directory, you can type:

```shell
pi@HAL:~$ cd ..
pi@HAL:/home$
```

There is also a shortcut to specify your own homedir, and that is by using the tilde `~`. You can immediately jump to your homedir by for example executing the following command:

```shell
pi@HAL:/$ cd ~
pi@HAL:~$
```
As this is used so much, the developers of the terminal decided to jump to the homedir when not specifying anything:

```shell
pi@HAL:/$ cd
pi@HAL:~$
```

## An Overview of the Linux Filesystem Layout

The first thing you need to know when viewing a Linux file system is that the file system is contained within a single tree, regardless of how many devices are incorporated.

What this means is that all components accessible to the operating system are represented somewhere in the main file system. If you use Windows as your primary operating system, this is different from what you are used to. In Windows, each hard drive or storage space is represented as its own file system, which are labeled with letter designations (C: being the standard top-level directory of the system file hierarchy and additional drives or storage spaces being given other letter labels).

In Linux, every file and device on the system resides under the "root" directory, which is denoted by a starting "/".

Thus, if we want to go to the top-level directory of the entire operating system and see what is there, we can type:

```shell
pi@HAL:/home$ cd /
pi@HAL:/$
```

Every file, device, directory, or application is located under this one directory. Under this, we can see the beginnings of the rest of the directory structure.

One of the principles guiding the organization of the file system is to allow it to be split across multiple disk partitions (or multiple disks) in a rational manner, and to allow appropriate pieces of it to be shared between machines. Key to this is the notion of the root partition (/, the parent of the entire file system).

When Linux boots, the kernel attaches a single file system partition all by itself. This is known as the root partition. Any other partitions that need to be attached are mounted by the mount command, usually under control of entries in the file "/etc/fstab". Because in the early stages of startup, only the root file system is available, it must contain everything needed for the system to function and attach the other pieces of the file system.

Tools on the root partition include the init program (which starts all the other processes), a shell, mount and the "/etc/fstab" file. The File System Hierarchy standard specifies a number of directories that must lie within the root partition.

Below is a typical Linux file system hierarchy.

![A typical Linux file system hierarchy](img/typical_filesystem_hierarchy.png)
:   A typical Linux file system hierarchy

Let's take a closer look at the different directories which can be found under the root.

**/bin** - This directory contains basic commands and programs that are needed to achieve a minimal working environment upon booting. These are kept separate from some of the other programs on the system to allow you to boot the system for maintenance even if other parts of the file system may be damaged or unavailable. If you search this directory, you will find that both ls and pwd reside here. The cd command is actually built into the shell we are using (bash), which is in this directory too.

**/boot** - This directory contains the actual files, images, and kernels necessary to boot the system. While /bin contains basic, essential utilities, /boot contains the core components that actually allow the system to boot. If you need to modify the bootloader on your system, or if you would like to see the actual kernel files and initial ramdisk (initrd), you can find them here. This directory must be accessible to the system very early on.

**/dev** - This directory houses the files that represent devices on your system. Every hard drive, terminal device, input or output device available to the system is represented by a file here. Depending on the device, you can operate on the devices in different ways. For instance, for a device that represents a hard drive, like /dev/sda, you can mount it to the file system to access it. On the other hand, if you have a file that represents a line printer like /dev/lpr, you can write directly to it to send the information to the printer.

**/etc** - Stands for "Editable Text Configuration". This is one area of the file system where you will spend a lot of time if you are working as a system administrator. This directory is basically a configuration directory for various system-wide services. By default, this directory contains many files and subdirectories. It contains the configuration files for most of the activities on the system, regardless of their function. In cases where multiple configuration files are needed, many times an application-specific subdirectory is created to hold these files. If you are attempting to configure a service or program for the entire system, this is a great place to look.

**/home** - This location contains the home directories of all of the users on the system (except for the administrative user, root). If you have created other users, a directory matching their username will typically be created under this directory. Inside each home directory, the associated user has write access. Typically, regular users only have write access to their own home directory. This helps keep the file system clean and ensures that not just anyone can change important configuration files.

Within the home directory, that are often hidden files and directories (represented by a starting dot) that allow for user-specific configuration of tools. You can often set system defaults in the /etc directory, and then each user can override them as necessary in their own home directory.

**/lib** - This directory is used for all of the shared system libraries that are required by the /bin and /sbin directories. These files basically provide functionality to the other programs on the system. This is one of the directories that you will not have to access often.

**/lost+found** - This is a special directory that contains files recovered by /fsck, the Linux file system repair program. If the file system is damaged and recovery is undertaken, sometimes files are found but the reference to their location is lost. In this case, the system will place them in this directory.

In most cases, this directory will remain empty. If you experience corruption or any similar problems and are forced to perform recovery operations, it's always a good idea to check this location when you are finished.

**/media** - This directory is typically empty at boot. Its real purpose is simply to provide a location to mount removable media (like cd’s). If your Linux operating system ever mounts a media disk and you are unsure of where it placed it, this is a safe bet.

**/mnt** - This directory is similar to the /media directory in that it exists only to serve as an organization mount point for devices. In this case, this location is usually used to mount file systems like external hard drives, etc.

This directory is often used in a VPS environment for mounting network accessible drives. If you have a file system on a remote system that you would like to mount on your server, this is a good place to do that.

**/opt** - This directory's usage is rather ambiguous. It is used by some distributions, but ignored by others. Typically, it is used to store optional packages. In the Linux distribution world, this usually means packages and applications that were not installed from the repositories.

For instance, if your distribution typically provides the packages through a package manager, but you installed program X from source, then this directory would be a good location for that software. Another popular option for software of this nature is in the /usr/local directory.

**/proc** - The /proc directory is actually more than just a regular directory. It is actually a pseudo-file system of its own that is mounted to that directory. The proc file system does not contain real files, but is instead dynamically generated to reflect the internal state of the Linux kernel.

This means that we can check and modify different information from the kernel itself in real time. For instance, you can get detailed information about the processor and its cores by typing

```shell
pi@HAL:/$ cat /proc/cpuinfo
processor       : 0
model name      : ARMv6-compatible processor rev 7 (v6l)
Features        : swp half thumb fastmult vfp edsp java tls
CPU implementer : 0x41
CPU architecture: 7
CPU variant     : 0x0
CPU part        : 0xb76
CPU revision    : 7

Hardware        : BCM2708
Revision        : 000e
Serial          : 000000008d79b8e3
```

**/root** - This is the home directory of the administrative user (called "root"). It functions exactly like the normal home directories, but is housed here instead.

**/run** - This directory is for the operating system to write temporary runtime information during the early stages of the boot process.

**/sbin** - This directory is much like the /bin directory in that it contains programs deemed essential for using the operating system. The distinction is usually that /sbin contains commands that are available to the system administrator, while the other directory contains programs for all of the users of the system.

**/selinux** - This directory contains information involving security enhanced Linux. This is a kernel module that is used to provide access control to the operating system.

**/srv** - This directory is used to contain data files for services provided by the system. In most cases, this directory is not used too much because its functionality can be implemented elsewhere in the filesystem.

**/tmp** - This is a directory that is used to store temporary files on the system. It is writable by anyone on the computer and does not persist upon reboot. This means that any files that you need just for a little bit can be put here. They will be automatically deleted once the system shuts down.

**/usr**  - Stands for Unix System Resources. This directory is one of the largest directories on the system. It basically includes a set of folders that look similar to those in the root / directory, such as /usr/bin and /usr/lib. This location is basically used to store all non-essential programs, their documentation, libraries, and other data that is not required for the most minimal usage of the system.

This is where most of the files on the system will be stored. Some important subdirectories are /usr/local, which is an alternative to the /opt directory for storing locally compiled programs. Another interesting thing to check out is the /usr/share directory, which contains documentation, configuration files, and other useful files.

**/var** - This directory is supposed to contain variable data. In practice, this means it is used to contain information or directories that you expect to grow as the system is used.

For example, system logs and backups are housed here. Another popular use of this directory is to store web content if you are operating a web server.

### Overview of Basic Filesystem Commands

The most used commands to traverse and manipulate the file system of a Linux system are listed in the table below. You can always use the man-command to get a detailed description.

|	Command |	Description									|
|-----------|-----------------------------------------------|
|	ls		|	List files									|
|	cp		|	Copy files									|
|	rm		|	Remove files								|
|	mv		|	Move files									|
|	cd		|	Change working dir							|
|	chmod	|	Change file permission mode					|
|	chown	|	Change owner of file						|
|	cat		|	Concatenate files and output to terminal	|
|	touch	|	Create an empty file						|
|	mkdir	|	Make directory								|


## Permissions and Ownership

Linux is a multi-user OS that is based on the Unix concepts of file ownership and permissions to provide security, at the file system level. It is essential that have a decent understanding of how ownership and permissions work.

### Linux Users

Linux is a multi-user system. A basic understanding of users and groups is required before ownership and permissions can be discussed, because they are the entities that the ownership and permissions apply to.

In Linux, there are two types of users: system users and regular users. Traditionally, system users are used to run non-interactive or background processes on a system, while regular users are used for logging in and running processes interactively.

An easy way to view all of the users on a system is to look at the contents of the "/etc/passwd" file. Each line in this file contains information about a single user, starting with its user name (the name before the first colon). Print the passwd file with the command:

```shell
pi@HAL:/$ cat /etc/passwd
```

Rendering the output:

```shell
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
...
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
libuuid:x:100:101::/var/lib/libuuid:
...
syslog:x:101:104::/home/syslog:/bin/false
kernoops:x:106:65534:Kernel Oops Tracking
bioboost:x:1000:1000:Nico De Witte,,,:/home/bioboost:/bin/bash
vboxadd:x:999:1::/var/run/vboxadd:/bin/false
```

### Super user

In addition to the two user types, there is the superuser, or root user, that has the ability to override any file ownership and permission restrictions. In practice, this means that the superuser has the rights to access anything on its own server. This user is used to make system-wide changes, and must be kept secure.

It is also possible to configure other user accounts with the ability to assume "superuser rights". In fact, creating a normal user that has sudo (superuser do) privileges for system administration tasks is considered to be best practice.

### Groups

Groups are collections of zero or more users. A user belongs to a default group (primary group), and can also be a member of any of the other groups on a server (secondary groups).

An easy way to view all the groups is to look in the "/etc/group" file.

```shell
pi@HAL:/$ cat /etc/group
```

Which renders something like this:

```shell
...
bluetooth:x:116:
colord:x:117:
pulse:x:118:
pulse-access:x:119:
mdm:x:120:
nopasswdlogin:x:121:
rtkit:x:122:
saned:x:123:
bioboost:x:1000:
...
```

By executing the `id` command you can also see to which groups an account belongs.

```shell
pi@HAL:/$ id bioboost
uid=1000(bioboost) gid=1000(bioboost) groups=1000(bioboost),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),108(lpadmin),110(sambashare)
```

### Viewing Ownership and Permissions

In Linux, each and every file is owned by a single user and a single group, and has its own access permissions.

The most common way to view the permissions of a file is to use `ls` with the long listing option, e.g.

```shell
pi@HAL:/$ ls -l <somefile>
```

If you want to view the permissions of all of the files in your current directory, run the command without an argument, like this

```shell
pi@HAL:~$ ls -l
```

Example output of this command is shown in the figure below.

![Output of ls -l command](img/output_ls_command.png)

You can also list the content of another directory without traversing to it but by specifying it as an argument to the `ls` command.

```shell
pi@HAL:~$ ls -al /etc/network
total 40
drwxr-xr-x   7 root root  4096 Jun 28 14:02 .
drwxr-xr-x 148 root root 12288 Aug 31 09:19 ..
drwxr-xr-x   2 root root  4096 Jun 28 14:35 if-down.d
drwxr-xr-x   2 root root  4096 Jun 28 14:36 if-post-down.d
drwxr-xr-x   2 root root  4096 Jun 28 14:36 if-pre-up.d
drwxr-xr-x   2 root root  4096 Jun 28 14:35 if-up.d
-rw-r--r--   1 root root    82 Aug 29 11:12 interfaces
drwxr-xr-x   2 root root  4096 Jan 24  2016 interfaces.d
```

The most important parts of this output are the filemode, the owner and the group of the files.

The following figure shows a break down of the filemode column into its components.

![File mode breakdown](img/filemode_breakdown.png)

The first character contain the file type and can be one of these:

* -: regular file
* d: directory (a file of a specific format that lists other files)
* l: a hard or soft link (basically a shortcut to another file)
* c: a character device file
* b: a block device file
* p: a pipe file
* s: a socket file

The next 9 characters make up the permission classes, namely user (owner), group, and other. The order of the classes is consistent across all Linux distributions.

The following users belong to each permissions class:

* User: The owner of a file belongs to this class
* Group: The members of the file's group belong to this class
* Other: Any users that are not part of the user or group classes belong to this class.

The next thing to pay attention to are the sets of three characters, or triads, as they denote the permissions, in symbolic form, that each class has for a given file.

In each triad, read, write, and execute permissions are represented in the following way:

* Read: Indicated by an r in the first position
* Write: Indicated by a w in the second position
* Execute: Indicated by an x in the third position. In some special cases, there may be a different character here.

A hyphen (-) in the place of one of these characters indicates that the respective permission is not available for the respective class.


Here is a quick breakdown of the access that the three basic permission types grant

* Read
	* For a normal file, read permission allows a user to view the contents of the file.
	* For a directory, read permission allows a user to view the names of the file in the directory.

* Write
	* For a normal file, write permission allows a user to modify and delete the file.
	* For a directory, write permission allows a user to delete the directory, modify its contents (create, delete, and rename files in it), and modify the contents of files that the user can read.

* Execute
	* For a normal file, execute permission allows a user to execute a file (the user must also have read permission). As such, execute permissions must be set for executable programs and shell scripts before a user can run them.
	* For a directory, execute permission allows a user to access, or traverse, into (i.e. cd) and access metadata about files in the directory (the information that is listed in an ls -l).

Something to note is that even though many permissions combinations are possible, only certain ones make sense in most situations. For example, write or execute access is almost always accompanied by read access, since it's hard to modify, and impossible to execute, something you can't read.

Let's see some examples

![Permissions Example](img/permissions_examples.png)

As you may have noticed, the owner of a file usually enjoys the most permissions, when compared to the other two classes. Typically, you will see that the group and other classes only have a subset of the owner's permissions (equivalent or less).

### Changing ownership and permissions

To change the ownership of files and directories the `chown` (Change Owner) and `chgrp` (Change Group) command can be used.
Permissions can be set using the `chmod` (Change Mode) command line tool.

You are encouraged to follow and try out the examples in the following sections.
Don't want to break anything ? Then simply create some test files in `/tmp`. They will
be automatically removed once the system is restarted.

Let's start with setting up a directory to host our files
```shell
$ mkdir -p /tmp/embedded_course && cd /tmp/embedded_course
```

Most examples are using files, however the procedure is exactly the same for a
directory (remember in Linux almost everything is file).

All examples can also be executed recursively by adding `-R` as an argument. This
will change the owner, group or mode (according to the issued command) for the given
directory and all files and other directories inside that specified directory.

#### Changing the owner of a file

The owner of a file or directory can be changed using the `chown` command.
To get some more information on the command you can use the man pages or execute
the command with a `--help` argument. This will output the following:

```shell
$ chown --help
Usage: chown [OPTION]... [OWNER][:[GROUP]] FILE...
  or:  chown [OPTION]... --reference=RFILE FILE...
Change the owner and/or group of each FILE to OWNER and/or GROUP.
```

First create a simple text file. The owner and group will be set according to the user
you used to create the file.

```shell
$ touch helloworld.txt
$ ls -al
total 8
drwxr-xr-x  2 bioboost bioboost 4096 Sep 30 09:15 .
drwxrwxrwt 15 root     root     4096 Sep 30 09:15 ..
-rw-r--r--  1 bioboost bioboost    0 Sep 30 09:15 helloworld.txt
```

Now let us change the owner to daemon

```shell
$ sudo chown daemon helloworld.txt
$ ls -al
total 8
drwxr-xr-x  2 bioboost bioboost 4096 Sep 30 09:15 .
drwxrwxrwt 15 root     root     4096 Sep 30 09:17 ..
-rw-r--r--  1 daemon   bioboost    0 Sep 30 09:15 helloworld.txt
```

#### Changing the group of a file

The group of a file or directory can also be changed using the `chown` command.

```shell
$ chown --help
Usage: chown [OPTION]... [OWNER][:[GROUP]] FILE...
  or:  chown [OPTION]... --reference=RFILE FILE...
Change the owner and/or group of each FILE to OWNER and/or GROUP.
```

The example below shows how the group of a file is changed to `root` using the `chown` command.
All you need to do is add a colon `:` before the name of the group.

```shell
$ sudo chown :root helloworld.txt
$ ls -al
total 8
drwxr-xr-x  2 bioboost bioboost 4096 Sep 30 09:15 .
drwxrwxrwt 15 root     root     4096 Sep 30 09:17 ..
-rw-r--r--  1 daemon   root        0 Sep 30 09:15 helloworld.txt
```

The `chown` command can also be used to both change the owner and group with a single
command.

The following example shows how to give back the ownership (both user and group)
to the `bioboost` user.

```shell
$ sudo chown bioboost:bioboost helloworld.txt
$ ls -al
total 8
drwxr-xr-x  2 bioboost bioboost 4096 Sep 30 09:15 .
drwxrwxrwt 15 root     root     4096 Sep 30 09:17 ..
-rw-r--r--  1 bioboost bioboost    0 Sep 30 09:15 helloworld.txt
```

The group of a file or directory can also be changed using the `chgrp` command.
To get some more information on the command you can use the man pages or execute
the command with a `--help` argument. This will output the following:

```shell
$ chgrp --help
Usage: chgrp [OPTION]... GROUP FILE...
  or:  chgrp [OPTION]... --reference=RFILE FILE...
Change the group of each FILE to GROUP.
```

The example below shows how to set the group to `root` for a specific file.

```shell
$ sudo chgrp root helloworld.txt
$ ls -al
total 8
drwxr-xr-x  2 bioboost bioboost 4096 Sep 30 09:15 .
drwxrwxrwt 15 root     root     4096 Sep 30 09:17 ..
-rw-r--r--  1 bioboost root        0 Sep 30 09:15 helloworld.txt
```

The following example shows how to give back the ownership (both user and group)
to the `bioboost` user, and this for the current directory and all files inside it.
This is accomplished by specifying that the command should do a recursive ownership
change.

```shell
$ sudo chown -R bioboost:bioboost .
$ ls -al
total 8
drwxr-xr-x  2 bioboost bioboost 4096 Sep 30 09:15 .
drwxrwxrwt 15 root     root     4096 Sep 30 09:17 ..
-rw-r--r--  1 bioboost bioboost    0 Sep 30 09:15 helloworld.txt
```

Be careful when using the recursive argument as it can really mess up your day,
especially in combination with the sudo prefix.

#### Changing permissions

On Linux and other Unix-like operating systems, there is a set of rules for each file which defines who can access that file, and how they can access it. These rules are called file permissions or file modes. The command `chmod` stands for "change mode", and it is used to define the way a file can be accessed.

In general, `chmod` commands take the form:

```shell
chmod <options> <permissions> <filename>
```

Permissions defines the permissions for the owner of the file (the "user"), members of the group who own the file (the "group"), and anyone else ("others"). There are two ways to represent these permissions: with symbols (alphanumeric characters), or with octal numbers (the digits 0 through 7).

##### Octal numbers

Here the digits 7, 5, and 4 each individually represent the permissions for the user, group, and others, in that order. Each digit is a combination of the numbers 4, 2, 1, and 0:
4 stands for "read",
2 stands for "write",
1 stands for "execute", and
0 stands for "no permission."

So continuing with the example file that was created before we could make the file
readable and writable by the user, readable by the group and inaccessible by others using
the following command:

```shell
$ chmod 640 helloworld.txt
$ ls -al
total 8
drwxr-xr-x  2 bioboost bioboost 4096 Sep 30 09:15 .
drwxrwxrwt 15 root     root     4096 Sep 30 10:17 ..
-rw-r-----  1 bioboost bioboost    0 Sep 30 09:15 helloworld.txt
```

##### Symbolic

The letters u, g, and o stand for "user", "group", and "other".
The equals sign ("=") means "set the permissions exactly like this," and the letters "r", "w", and "x" stand for "read", "write", and "execute", respectively.
The commas separate the different classes of permissions, and there are no spaces in between them.

The equal sign can also be replaced by a plus sign ("+") or a minus sign ("-"). This respectively adds the permissions or removes permissions for the user, group or others.

Let's make the hello world file readable and writeable by the owner and
group and readable by everyone:

```shell
$ chmod u=rw,g=rw,o=r helloworld.txt
$ ls -al
total 8
drwxr-xr-x  2 bioboost bioboost 4096 Sep 30 09:15 .
drwxrwxrwt 15 root     root     4096 Sep 30 10:17 ..
-rw-rw-r--  1 bioboost bioboost    0 Sep 30 09:15 helloworld.txt
```

Next we remove the write permissions for the group and the owner:

```shell
$ chmod u-w,g-w helloworld.txt
$ ls -al
total 8
drwxr-xr-x  2 bioboost bioboost 4096 Sep 30 09:15 .
drwxrwxrwt 15 root     root     4096 Sep 30 10:17 ..
-r--r--r--  1 bioboost bioboost    0 Sep 30 09:15 helloworld.txt
```

Last the file should be readable and writeable by the user, readable by the group and
inaccessible by everyone else.

```shell
$ chmod u+w,o-r helloworld.txt
$ ls -al
total 8
drwxr-xr-x  2 bioboost bioboost 4096 Sep 30 09:15 .
drwxrwxrwt 15 root     root     4096 Sep 30 10:17 ..
-rw-r-----  1 bioboost bioboost    0 Sep 30 09:15 helloworld.txt
```

## Debian and it's Packages

Every Linux distribution is different in terms of how software is installed. Linux distributions use different installation file types, package managers, and commands for installation. Even within a single form of Linux, there are different types of package managers.

Debian files are usually downloaded by package managers from a software repository. A repository is a collection of Debian files that typically comes from a server or other location. Package managers access these repositories and download the requested Debian file. Then, the package manager installs the package. A package manager is software used to handle the installation, removal, configuration, and updating of programs and drivers on a computer system. If a Debian file is not downloaded from a repository, then the user downloaded or created a Debian file. The local file can still be installed; Debian files are not required to come from a repository, although most do.

Packages generally contain all of the files necessary to implement a set of related commands or features. There are two types of Debian packages:

* **Binary packages**, which contain executables, configuration files, man/info pages, copyright information, and other documentation. These packages are distributed in a Debian-specific archive format; they are usually distinguished by having a '.deb' file extension. Binary packages can be unpacked using the Debian utility dpkg (possibly via a frontend like aptitude).
* **Source packages**, which consist of a .dsc file describing the source package (including the names of the following files), a .orig.tar.gz file that contains the original unmodified source in gzip-compressed tar format and usually a .diff.gz file that contains the Debian-specific changes to the original source. The utility dpkg-source packs and unpacks Debian source archives. (The program apt-get can be used as a frontend for dpkg-source.)

Installation of software by the package system uses "dependencies" which are carefully designed by the package maintainers. These dependencies are documented in the control file associated with each package.

For example, the package containing the GNU C compiler (gcc) "depends" on the package binutils which includes the linker and assembler. If a user attempts to install gcc without having first installed binutils, the package management system (dpkg) will send an error message that it also needs binutils, and stop installing gcc.

There are multiple tools that are used to manage Debian packages, from graphic or text-based interfaces to the low level tools used to install packages. All the available tools rely on the lower level tools to properly work.

It is important to understand that the higher level package management tools such as aptitude or dselect rely on apt which, itself, relies on dpkg to manage the packages in the system.

### DPKG

Dpkg is the main package management program.

### APT

APT is the Advanced Package Tool and provides the apt-get program. apt-get provides a simple way to retrieve and install packages from multiple sources using the command line. Unlike dpkg, apt-get does not understand .deb files, it works with the packages proper name and can only install .deb archives from a source specified in /etc/apt/sources.list. apt-get will call dpkg directly after downloading the .deb archives from the configured sources.

Some common ways to use apt-get are:

* To update the list of package known by your system, you can run:

```shell
$ apt-get update
```

(you should execute this regularly to update your package lists)

* To upgrade all the packages on your system (without installing extra packages or removing packages), run:

```shell
$ apt-get upgrade
```

* To install the foo package and all its dependencies, run:

```shell
$ apt-get install foo
```

* To remove the foo package from your system, run:

```shell
$ apt-get remove foo
```

* To remove the foo package and its configuration files from your system, run:

```shell
$ apt-get purge foo
```

* To upgrade all the packages on your system, and, if needed for a package upgrade, installing extra packages or removing packages, run:

```shell
$ apt-get dist-upgrade
```

### Aptitude

Aptitude is a package manager for Debian GNU/Linux systems that provides a frontend to the apt package management infrastructure. Aptitude is a text-based interface using the curses library, it can be used to perform management tasks in a fast and easy way.

* aptitude offers easy access to all versions of a package.
* aptitude makes it easy to keep track of obsolete software by listing it under "Obsolete and Locally Created Packages".
* aptitude includes a fairly powerful system for searching particular packages and limiting the package display. Users familiar with mutt will pick up quickly, as mutt was the inspiration for the expression syntax.
* aptitude can be used to install the predefined tasks  available.
* aptitude in full screen mode has su functionality embedded and can be run by a normal user. It will call su (and ask for the root password, if any) when you really need administrative privileges

Aptitude is most commonly used for searching for packages. You can use the following command for this:

```shell
pi@HAL:/$ aptitude search foobar
```

You can launch the 'graphical' frontend by running it from the terminal:

```shell
pi@HAL:/$ aptitude
```
