# yocto-commands

## Kernel commands

To build kernel. Based on kernel we are using:
`
bitbake linux-yocto
or
bitbake linux-imx
or
bitbake linux-intel
`
To compile specific bb file:
`
bitbake -b <bb file full path>
`
To clean local state but keep downloaded image
`
bitbake -c cleansstate linux-yocto
`
To clean everything, next compilation will again download the source code
`
bitbake -c cleanall linux-yocto
`
Selectavely compiled modules doesn't get into rootfs. To add it in rootfs, 1st clean state and then rebuild the target. It will re-generate the rootfs and so image.
`
bitbake -c cleansstate <target name>
bitbake <target name>
`
To run kernel menuconfig.
`
bitbake -c menuconfig linux-yocto
`
## Devshell

To run specific commands such as do_compile, for a target in openembedded environment, devshell could be used.
`
bitbake -c devshell <target>
`
This opens up devshell terminal in new window by going into target location. And on that we we can execute commands for development/debugging.

`
bitbake -c devshell linux-yocto
`
In new devshell we can give commands as working on it locally, e.g.:
`
make menuconfig
make
`
https://www.openembedded.org/wiki/Devshell

## To create customized config for kernel
`
bitbake linux-yocto -c menuconfig
`
Do the needed changes and save. And create diffconfig, which will be a .cfg file. Let's say, gpio.cfg
`
bitbake linux-yocto -c diffconfig
`

Create customized layer
`
mkdir -p custom-layer/recipes-kernel/linux/linux-yocto/files
cp <>/gpio.cfg custom-layer/recipes-kernel/linux/linux-yocto/files/
touch custom-layer/recipes-kernel/linux/linux-yocto/linux-yocto_%.bbappend
echo >> FILESEXTRAPATHS_prepend := "${THISDIR}/files:"
echo >> SRC_URI += "file://gpio.cfg"
`
Now, bitbaking linux-yocto will include these changes, once custom-layer is added in local/bblayer.conf file.

There had been issues where compilation doesn't work for 32 bit, x86, system. With the error,

* wic
We have created images for the target, bootloader, kernel, initramfs, rootfs, etc, not necessarily all but depends on target. Now we need to flash all these into a bootable medium, mmc, usb, etc. Ether we can flash or copy all seperately into the bootable medium or we can use `wic` tool provided by openembedded. Wic takes the target imaged built and create ready to `dd` image. wic has several options as well to customize file system, such as where to place bootloader into file system, where to place kernel, etc. Below is the simple command to create `dd`able image. For any customization, check wic help.

`
wic <taget image name> -e <bitbaked target name>
`

## References
https://community.nxp.com/docs/DOC-100847
