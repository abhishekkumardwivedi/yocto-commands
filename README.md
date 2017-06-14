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
If OE environment is messed up with host environment during compilation (for me, 32 bit target device kernel image was reluctant to compile in 64 bit build system), add devshell as bitbake command argument. Better use it in error scenario, as this does open new shell and hides all generic logs of execution with do_devshell.

`
bitbake -c devshell <target>
`

This resolved this error for me while compiling for Galilieo Gen2.
`
error: code model 'kernel' not supported in the 32 bit mode
`

https://www.openembedded.org/wiki/Devshell

There had been issues where compilation doesn't work for 32 bit, x86, system. With the error,

## References
https://community.nxp.com/docs/DOC-100847
