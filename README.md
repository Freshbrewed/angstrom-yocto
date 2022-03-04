# Ångström-Yocto-QEMU image

Initialized Yocto project with all required dependencies to build a working Ångström Linux image successfully to be run using Yocto's "tool-set" QEMU. 
You only have to clone this repository, run a baking command to create your own working Ångström image and start emulating it using provided QEMU.

## Purpose
Official Ångström Linux distribution is no longer maintained and information regarding it is scattered all around. 
There are lots of dead links or dependencies leading to dead links which makes it hard to build and emulate a working image.
The objective is to combine all the working links, methods, tools and dependencies into a single repository where we can start baking Ångström image right away.

You may fiddle with local.conf file however you wish, or add extra layers to be used by bitbake but the defaults set in this repository results in a working image.
Trial and error!

## Build configuration
* YOCTO_RELEASE = THUD
* BB_VERSION = 1.40.0
* BUILD_SYS = x86_64-linux
* TARGET_SYS = x86_64-angstrom-linux
* MACHINE = qemux86-64
* DISTRO = angstrom
* DISTRO_VERSION = v2018.12
* TUNE_FEATURES = m64 core2

## Image specifications
* DISTRO: Ångström Linux v2018.12
* IMAGE SIZE: 5GB (can be manually configured)
* KERNEL: 4.18.33

If you want to change the image size, locate local.conf file from
<code>cd build/conf</code> and edit the last line <code>IMAGE_ROOTFS_EXTRA_SPACE_append = " + 5000000"</code> where **5000000** is the image size.   

## Preparation
Building is the most time consuming operation which varies on the processing power of your processor. 
A processor with 2 cores and 4 threads bitbakes a working Ångström image in around 6 hours.

**BEWARE. You need AT LEAST 20GB of disk space.**
Procedure takes lots of disk space since every single component has to be downloaded, extracted and baked inside the system image. 
Once the procedure is over, you may free up space by deleting cache, backups and downloads inside the project, leaving you only with a system image.

Ubuntu/Debian dependencies
```bash
sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib build-essential chrpath socat libsdl1.2-dev xterm
```
Cloning the repository
```bash
git clone git://github.com/Freshbrewed/angstrom-yocto angstrom-yocto
```
## Building
Make sure to source files inside angstrom-yocto folder:
```bash
source oe-init-build-env
```
To start baking Ångström Linux distribution 
```bash
bitbake core-image-full-cmdline
```
In case you are in dire need of conserving some space, you can run a command to build a minimalist version of the system image.
```bash
bitbake core-image-minimal
```
Bitbaked images reside in **angstrom-yocto/build/tmp-glibc/deploy/images/~**
## Usage
Running QEMU inside Yocto-project
```bash
runqemu qemux86-64
```
The default password for the user is **root**. The image will have networking capabilities.
