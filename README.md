# Nitrogen6x Gadget Snap

This repository contains the source for an Ubuntu Core gadget snap
for the Nitrogen6x. Building it with snapcraft will
automatically pull, configure, patch and build the git.denx.de/u-boot.git
upstream source for `nitrogen6q2g_defconfig` at release `v2018.11` and produce
a bootable gadget snap with the resulting binaries.

## Gadget Snaps

Gadget snaps are a special type of snaps that contain device specific support
code and data. You can read more about them in the snapd wiki
https://github.com/snapcore/snapd/wiki/Gadget-snap

## Building

### Cross on x86 systems

Just run snapcraft in the top of the srouce tree.

```
snapcraft
```

## Update U-boot image in SPI-Flash

Nitrogen6x won't boot bootloader from SDcard or USB
You will need to do following step to update onboard SPI Flash

Copy the stoc u-boot.imx from gadget snap to /system-boot/ partition
then inset to SD slot on Nitroge6X board 

U-Boot > fatload mmc 0:1 0x13000000 u-boot.imx;sf probe;sf erase 0 0xc2000;sf write 0x13000000 0x400 ${filesize}

and update env...

U-Boot > fatload mmc 0:1 0x13000000 nitrogen6x-kernel_x1.snap/dtbs/imx6q-nitrogen6x.dtb;env import 0x13000000;env save;reset

