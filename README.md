# MP30AR0-Installation

## Intro

Author: Yu-Chiang Huang <tjjh89017@hotmail.com>

## Installation

### Requirement

* UEFI bootloader
* Console Wire
* CentOS 7 AArch64 installation iso (Optional)
* Cross-compile environment for AArch64 Linux Kernel

### Prepare

* Ubuntu Xenial AArch64 UEFI PXE installer
* Patched `apm-mp30ar0.dtb`

### Installation

#### Note: USB is totally DEAD

Using UEFI shell to set MAC address for NIC

Patch Ubuntu kernel `CONFIG_NET_XGENE=m` to `CONFIG_NET_XGENE=y`, and build it. Replace Ubuntu installer kernel with the patched one. Boot it and install Ubuntu with parch DTB. Install patched kernel into Ubuntu rootfs.

#### To be continued
