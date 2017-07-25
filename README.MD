# Linux Live Kit Improved.
This set of scripts will help you to 
build your own Live Kit distro. This project is based on 
the original Linux Live Kit. <http://linux-live.org>

### Here's what you need to do:
Please note: 
Make sure to extract and use it on a POSIX-compatible filesystem,
since it creates some (sym)links and such.

### Here's you what you need to watch out before building:
+ Store Linux Live Kit in a directory which is not going to be included
  in your live distro, else it would be copied to it. Best practice is to
  make a directory such as /tmp/a and put all the files there.

+ Before you start building your Kit, edit the ./.config file
  Most importantly change the LIVEKITNAME variable.

+ Make sure your kernel is in /boot/vmlinuz or change the path in ./.config
  Your kernel must support squashfs and aufs. 
  Debian Jessie's kernel has both supported out-of-the-box.

+ You may also wish to replace boot background in ./bootfiles/bootlogo.png, 
  and reorganize syslinux.cfg to fit your needs. 
Please note: 
  When editing the .cfg file, make sure to keep all paths pointing to /boot/, since 
  it will be replaced to /LIVEKITNAME/boot/ during the build session.

+ Linux Live Kit comes with precompiled static binaries in ./initramfs
  directory. Those may be outdated but will work. You may replace them
  by your own statically linked binaries, if you know how to compile them.

+ If you want to boot your Live Kit from a CD, you need to recompile
  syslinux.bin/isolinux.bin else it won't be able to boot your Live Kit 
  from directory "/LIVEKITNAME". There is a script prepared for you which 
  will handle all of the building. Simply go to directory ./tools/ and run 
  update-isolinux.bin, it will rebuild ./bootfiles/isolinux.bin automatically 
  by downloading SysLinux sources, patching them using your actual LIVEKITNAME and
  recompiling. This step is not needed if you plan only need the ZIP archive version.

+ If you have tmpfs mounted on /tmp, make sure you have enough (or maybe even 
  a lot of) RAM, since Live Kit will store lots of data to the target. 
  If you don't have enough (or even went out of) RAM, make sure 
  /tmp is a regular on-disk directory.

+ When done, run the ./build script to create your Live Kit
  - it will create ISO and ZIP files for you in /tmp
  - make sure you have enough free space in /tmp to handle it

+ You will need the following packages to be installed:
  - squashfs-tools
  - genisoimage or mkisofs
  - zip