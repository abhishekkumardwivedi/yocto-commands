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

## References
https://community.nxp.com/docs/DOC-100847
