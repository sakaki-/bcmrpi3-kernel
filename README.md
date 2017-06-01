# bcmrpi3-kernel
Automated build of the latest 64-bit `bcmrpi3_defconfig` Linux kernel for the Raspberry Pi 3 model B, updated weekly.

Currently tracking the 4.9.y branch, as this is receiving VC4 backports etc.

Variant | Version | Most Recent Image
:--- | ---: | ---:
Kernel, dtbs, modules and (kernel) firmware | a.b.c.d | [bcmrpi3-kernel-a.b.c.d.tar.xz](https://github.com/sakaki-/bcmrpi3-kernel/releases/download/a.b.c.d/bcmrpi3-kernel-a.b.c.d.tar.xz)

> The older images are still available [here](https://github.com/sakaki-/bcmrpi3-kernel/releases).

To deploy (assuming that your RPi3's micro SD-card's first partition is mounted as `/boot`, and you are already running a 64-bit RPi3 image, such as my [gentoo-on-rpi3-64bit](https://github.com/sakaki-/gentoo-on-rpi3-64bit)) simply download, untar into the root directory, and reboot:
```console
pi64 ~ # cp /boot/kernel8.img{,.old}
pi64 ~ # wget -c https://github.com/sakaki-/bcmrpi3-kernel/releases/download/a.b.c.d/bcmrpi3-kernel-a.b.c.d.tar.xz
pi64 ~ # tar -xJf bcmrpi3-kernel-a.b.c.d.tar.xz -C /
pi64 ~ # sync && reboot
```
These prebuilt kernels are provided as a convenience only. Use at your own risk!
