# bcmrpi3-kernel
Automated build of the latest 64-bit `bcmrpi3_defconfig` Linux kernel for the Raspberry Pi 3 model B, updated weekly.

## Description

<img src="https://raw.githubusercontent.com/sakaki-/resources/master/raspberrypi/pi3/Raspberry_Pi_3_B.jpg" alt="Raspberry Pi 3 B" width="250px" align="right"/>

This project contains a weekly autobuild of the default branch of the [official Raspberry Pi Linux source tree](https://github.com/raspberrypi/linux), for the [64-bit Raspberry Pi 3 Model B](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/).

Builds are performed with the standard `bcmrpi3_defconfig`, with the only change being that the first 12 hex digits of the tip commit SHA1 hash are appended to `CONFIG_LOCALVERSION` (with a separating hyphen) before building. A new build tarball is automatically created and uploaded as a release asset each week (unless the tip of the default branch is unchanged from the prior week, or an error occurs during the build process).

> The default branch is used, as that is generally given most attention for e.g. VC4 backports.

For example, on 1 June 2017, the default branch was `rpi-4.9.y` and the latest commit was `e5bd734340e6871e4e9ef5ff66e61197eb8ece30` (the short form of which is `e5bd734340e6`). The created release was [4.9.30.20170601](https://github.com/sakaki-/bcmrpi3-kernel/releases/4.9.30.20170601), within which the kernel tarball was `bcmrpi3-kernel-4.9.30.20170601.tar.xz`, and the corresponding kernel release name was `4.9.30-v8-e5bd734340e6+`.

Each kernel release tarball provides the following files:
* `/boot/kernel8.img` (this is the bootable 64-bit kernel);
* `/boot/bcm-2710-rpi-3-b.dtb` and `/boot/bcm-2837-rpi-3-b.dtb` (the device tree blobs);
* `/lib/modules/<kernel release name>/...` (the module set for the kernel);
* `/lib/firmware/...` (the kernel-built firmware).

The current kernel tarball may be downloaded from the link below (or via `wget`, or via the corresponding `bcmrpi-kernel-bin` ebuild, per the [instructions following](#installation)):

Variant | Version | Most Recent Image
:--- | ---: | ---:
Kernel, dtbs, modules and (kernel) firmware | 4.9.48.20170911 | [bcmrpi3-kernel-4.9.48.20170911.tar.xz](https://github.com/sakaki-/bcmrpi3-kernel/releases/download/4.9.48.20170911/bcmrpi3-kernel-4.9.48.20170911.tar.xz)

The corresponding kernel configuration (derived via `make bcmrpi3_defconfig`) may be viewed [here](https://github.com/sakaki-/bcmrpi3-kernel/blob/master/config).

> A list of all releases may be seen [here](https://github.com/sakaki-/bcmrpi3-kernel/releases).

## <a name="installation"></a>Installation

To deploy (assuming that your RPi3's micro SD-card's first partition is mounted as `/boot`, and you are already running a 64-bit RPi3 image, such as my [gentoo-on-rpi3-64bit](https://github.com/sakaki-/gentoo-on-rpi3-64bit)) simply download, untar into the root directory, and reboot:
```console
pi64 ~ # cp /boot/kernel8.img{,.old}
pi64 ~ # wget -c https://github.com/sakaki-/bcmrpi3-kernel/releases/download/4.9.48.20170911/bcmrpi3-kernel-4.9.48.20170911.tar.xz
pi64 ~ # tar -xJf bcmrpi3-kernel-4.9.48.20170911.tar.xz -C /
pi64 ~ # sync && reboot
```

Alternatively, if you have my [rpi3 overlay](https://github.com/sakaki-/rpi3-overlay) installed (it is pre-installed on the [gentoo-on-rpi3-64bit](https://github.com/sakaki-/gentoo-on-rpi3-64bit) image), you can simply emerge the `bcmrpi3-kernel-bin` package (a new ebuild is automatically created to mirror each release here). For example, to install the latest available version (and start using it):
```console
pi64 ~ # emaint sync --repo rpi3
pi64 ~ # emerge -av bcmrpi3-kernel-bin
pi64 ~ # reboot
```

Or, to install a particular version (e.g.):
```console
pi64 ~ # emaint sync --repo rpi3
pi64 ~ # emerge -av =bcmrpi3-kernel-bin-4.9.30.20170601
pi64 ~ # reboot
```

> NB: these prebuilt kernels and ebuilds are provided as a convenience only. Use at your own risk! **Given that the releases in this project are created automatically, there is no guarantee that any given kernel will boot correctly.** A 64-bit kernel is necessary, but not sufficient, to boot the RPi3 in 64-bit mode; you also need the supporting firmware, configuration files, and userland software (see for example my [gentoo-on-rpi3-64bit](https://github.com/sakaki-/gentoo-on-rpi3-64bit) project, or Neddy's Seagoon's [Raspberry Pi 3 64 bit Install](https://wiki.gentoo.org/wiki/Raspberry_Pi_3_64_bit_Install) page on the Gentoo wiki, for more information).
