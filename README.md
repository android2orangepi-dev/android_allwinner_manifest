# Manifest for Allwinner Android

This version is based on [Android 10.0.0 Release 2](https://android.googlesource.com/platform/manifest/+/refs/heads/android-10.0.0_r2).

## For customization we use the follov parameters:
* Customer - **Allwinner**
* Supported platform - **Orange Pi Plus 2E**

## There are added the follow new projects:
| Location | Repo Link | Branch/Tags |
| ------ | ------ | ------ |
| external/mesa3d | [repo](https://github.com/android2orangepi-dev/mesa) | refs/tags/OrangePlus2e_AndroidQ_preview2 |
| external/uboot | [repo](http://git.denx.de/u-boot.git_mainline) | refs/tags/v2019.10-rc3 |
| external/gbm_gralloc | [repo](https://github.com/android2orangepi-dev/gbm_gralloc) | refs/tags/OrangePlus2e_AndroidQ_preview2 |
| device/allwinner | [repo](https://github.com/android2orangepi-dev/android_allwinner_bsp) | refs/tags/OrangePlus2e_AndroidQ_preview2 |
| kernel/allwinner | [repo](https://android.googlesource.com/kernel/common) | refs/tags/OrangePlus2e_AndroidQ_preview2 |
| prebuilts/gcc/linux-x86/arm/gcc-linaro_arm-linux-gnueabihf | [repo](https://github.com/android2orangepi-dev/ext-compiler) | refs/tags/OrangePlus2e_AndroidQ_preview1 |

## Install necessaty tools for building under Ubuntu
For Android build You need to set up your local work environment according [Google's recommendations](https://source.android.com/setup/build/initializing). Probably You need to install additional packets.

```bash
sudo apt-get install swig lz4 repo python-dev python3-dev libssl-dev
pip install Mako
```
 
## Fetching Android sources
```bash
mkdir -p ${ANDROID_ROOT}
cd ${ANDROID_ROOT}/
```

### SSH
```bash
repo init -u git@github.com:android2orangepi-dev/android_allwinner_manifest -b refs/tags/OrangePlus2e_AndroidQ_preview2 -m ssh.xml
repo sync -cq
```

### HTTPS
```bash
repo init -u https://github.com/android2orangepi-dev/android_allwinner_manifest -b refs/tags/OrangePlus2e_AndroidQ_preview2 -m https.xml
repo sync -j1 -cq
```

## Android build
### Building
```bash
cd ${ANDROID_ROOT}/
export NUM_JOBS=$(($(grep ^processor /proc/cpuinfo | wc -l)*2))
. ./build/envsetup.sh
lunch orangepi_plus2e-userdebug
make -j${NUM_JOBS} 2>&1 | tee ../android_build.log
```

## Deployment
### SDCard
For sdcard image build You can use existed target:
 
```bash
cd ${ANDROID_ROOT}/
make sdcard
```

Please use sdcard.img (out/target/product/plus2e/sdcard.img) for flashing to SD Card (Please replace X for a correct letter in sdX).

```bash
cd ${ANDROID_ROOT}/
export card=/dev/sdX
dd if=out/target/product/plus2e/sdcard.img of=${card} bs=4096
sync
```
