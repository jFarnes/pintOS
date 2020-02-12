# pintOS
Proyecto pintOS de ciencias de la computacion 7 - Universidad Galileo

Installing PintOS on QEMU
Pintos – Installation
I am currently doing an operating systems course that requires me to work with pintos – an educational operating system for the x86. Needless to say, I started scouring the Internet for tutorials in order to run it on my system. I found a few, but they are a bit outdated; pintos code seems to have changed a little over time. The methods specified on the official Stanford page cover everything but are a little cryptic. So here I am, outlining steps to get pintos up and running on your system.
Pintos code has been written to run on Unix based systems, “not designed to install under any form of Windows”. I have tested the steps on Linux Mint 14 – Nadia and Ubuntu 12.04. There should be minimal changes for other distros, mostly in places where installation of packages is required from the software repository.

Prerequisites

The following packages need to be installed on your system:
1. GCC
2. GNU binutils
3. Perl
4. GNU make
5. QEMU; “If QEMU is not available, Bochs can be used, but its slowness is frustrating.”
6. GDB

Installation

In the subsequent text, $HOME will refer to your home directory, wherever you create a folder for pintos.
Once the prerequisites have been installed, do the following steps:

1. Download Pintos:
Download the pintos source code here . Extract it in some directory, say $HOME/os .

2. Set GDBMACROS
Open the script ‘pintos-gdb’ (in $HOME/os/pintos/src/utils) in any text editor. Find the variable GDBMACROS and set it to point to $HOME/os/pintos/src/misc/gdb-macros .
Remember to replace $HOME with the actual path.

3. Compile the utilities
Change to the utils folder, if not already there, and compile the utilities by typing

make

on the terminal.
If you get an error saying “Undefined reference to ‘floor’ “, make the following changes; edit ‘Makefile’ in the current directory and replace “LDFLAGS = -lm” by “LDLIBS = -lm”. Recompile now, it will work.

4. Edit Make.vars in /threads
Edit the file ‘Make.vars’ in the ‘threads’ directory ( $HOME/os/pintos/src/threads ); change the last line to:
SIMULATOR = –qemu

5. Compile Pintos kernel
Change to the ‘threads’ directory, if not already there, and run ‘make’ to compile the pintos kernel.

6. Edit the pintos utility
Make these changes in the ‘pintos’ file at $HOME/os/pintos/src/utils/’:
a) On line number 103, change ‘bochs’ to ‘qemu’.
b) On line number 259, change ‘kernel.bin’ to the actual path at ‘$HOME/os/pintos/src/threads/build/kernel.bin’.

7. Edit pintos.pm file
Open the file ‘$HOME/os/pintos/src/utils/Pintos.pm’ in the editor and at line number 362, change “loader.bin” to the actual path to the file at ‘$HOME/os/pintos/src/threads/build/loader.bin’.

8. Create qemu link
You need to create a link to the QEMU executable on your system; these will generally be found in ‘/usr/bin’. If it is not there search the $PATH folders for it. Whichever directory you find it, change to that directory and type the following command:

ln -s qemu-system-i386 qemu

This will create a link ‘qemu’ to the QEMU executable.
Restart the terminal for changes to take effect.

9. Run Pintos
Go to the ‘utils’ directory at ‘$HOME/os/pintos/src/utils/’ and run pintos with the following command:

./pintos run alarm-multiple

Now you are all set to get hacking away with Pintos.
If you face some errors or have doubts, please feel free to comment below.

Acknowledgement
This is the site that got me started:
http://pintosiiith.wordpress.com/2012/09/13/install-pintos-with-qemu/ . I have merely organized all the information I found here.

This post was referenced from
http://krharsha.blogspot.in/2013/08/pintos-installation.html