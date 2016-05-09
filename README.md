# MP30AR0-Installation

## Intro

Author: Yu-Chiang Huang <tjjh89017@hotmail.com>

## Installation

### Requirements

* UEFI Bootloader
* Console Wire
* Installation ISO, just pick up one:
  * CentOS 7 AArch64
  * Fedora 23 AArch64

### Prepare

#### UEFI Bootloader

[Here](https://rwmj.wordpress.com/2016/03/08/gigabyte-mp30-ar0-flashing-uefi/)
is a tutorial about flashing UEFI bootloader.

Also, remember to set MAC address in UEFI shell.

i.e.
```
set MAC0 aa:bb:cc:dd:ee:01
set MAC1 aa:bb:cc:dd:ee:02
```

#### Installation ISO

Choosing a installation media is a big deal.
The media should support by the kernel.
For example, cnosider a tragedy senario,
we have a USB stick shipped a fabulous Linux distro.
Then we plug it into our board and UEFI reconizes it, great!
So we boot our USB instantly. The kernel is loaded into memory and...
none of filesystem mounted, because of lack of USB driver.

It seems that in there is lack of USB drive in some older 
linux distro aarch64 installation ISO.
(Maybe in the newer release it won't be an issue)
So we just take a harddisk,
turn it into installation disk and dance with SATA.

1. Get the ISO from
   [Fedora 23](http://dl.fedoraproject.org/pub/fedora-secondary/releases/23/Server/aarch64/iso/) or
   [CentOS 7.2](http://mirror.centos.org/altarch/7.2.1603/isos/aarch64/)
2. Make sure that the md5 checksum is matched.
3. Prepare a installation harddisk.
   The command `dd` can save our life.

```shell
sudo dd if=/path/to/Fedora.iso of=/dev/sdX bs=1M conv=fsync
```

And then connect the harddisk via SATA.

### Installation

#### UEFI

Boot installation ISO from UEFI shell. Check for installation disk is `FS0` or `FS1`.

```
FS1:\EFI\BOOT\BOOTAA64.efi
```

#### GRUB

We don't need to modify anything in GRUB.

#### Installation Process

**NOTE: You must have a Console wire to connect ttyS0**

VGA ports won't display any installation option but display only kernel log.
Using console to start VNC mode or install Linux in text mode.

```
screen /dev/ttyS0 115200
```

## Known Issue

### Virtualization

KVM works fine.

Xen status unknown.

### PCIe
PCIe doesn't work fine. We can download MP30AR0 devicetree from [offical website](http://b2b.gigabyte.com/products/product-page.aspx?pid=5422#dl)

### SFP+
Only one port works. To enable another port, download MP30AR0 devicetree from [offical website](http://b2b.gigabyte.com/products/product-page.aspx?pid=5422#dl)

### ACPI
ACPI only works on CentOS, RHELSA, but Fedora.

## Reference

[Richard WM Jones Blogs](https://rwmj.wordpress.com)
