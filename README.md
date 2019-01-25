# android_sunxi_manifest
Manifest for building Android for Sunxi vendor 

There is fork of AOSP Manifest, updating on 23.01.2019

## For customization wue use the follov parameters:
- customer = sunxi
- platform = orangepih3

## There are added the follow a new projects:
* vendor->sunxi: (https://github.com/android2orangepi-dev/android_sunxi_vendor, branch master)
* vendor->sunxi->external:(https://github.com/android2orangepi-dev/u-boot_mainline_fork, branch android-sunxi)
* device->sunxi: (https://github.com/android2orangepi-dev/android_sunxi_bsp, branch master)
* hardware->sunxi: (https://github.com/android2orangepi-dev/android_sunxi_hardware, branch master)
* kernel->sunxi: (https://github.com/android2orangepi-dev/linux, branch android-sunxi)
