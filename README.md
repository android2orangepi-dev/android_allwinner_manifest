# Manifest for Allwinner Android

This version is based on Android 9.0.0 [Release 30 (PQ1A.190105.004)](https://android.googlesource.com/platform/manifest/+/refs/heads/android-9.0.0_r30/default.xml).

## For customization we use the follov parameters:
* Customer - **Allwinner**
* Supported platform - **Orange Pi Plus 2E**

## There are added the follow new projects:
| Location | Repo Link | Branch |
| ------ | ------ | ------ |
| vendor/allwinner | [repo](https://github.com/android2orangepi-dev/android_allwinner_vendor) | master |
| vendor/u-boot | [repo](https://github.com/android2orangepi-dev/u-boot_mainline_fork) | android-allwinner |
| device/allwinner | [repo](https://github.com/android2orangepi-dev/android_allwinner_bsp) | master |
| hardware/allwinner | [repo](https://github.com/android2orangepi-dev/android_allwinner_hardware) | master |
| kernel/allwinner | [repo](https://github.com/android2orangepi-dev/linux) | android-allwinner |
| prebuilts/gcc/linux-x86/arm/gcc-linaro_arm-linux-gnueabihf | [repo](https://github.com/android2orangepi-dev/ext-compiler) | master |
 
## Fetching Android sources
```bash
mkdir -p ${ANDROID_ROOT}
cd ${ANDROID_ROOT}/
```

### SSH
```bash
repo init -u git@github.com:android2orangepi-dev/android_allwinner_manifest -b android-allwinner -m ssh.xml
repo sync
```

### HTTPS
```bash
repo init -u https://github.com/android2orangepi-dev/android_allwinner_manifest -b android-allwinner -m https.xml
repo sync -j1
```

### Install necessaty tools for building under Ubuntu
```bash
sudo apt-get install swig
sudo apt-get install python-dev python3-dev
sudo apt-get install libssl-dev
```

### Android build
```bash
mkdir ~/mydroid 
export PATH=$(pwd):${PATH}
export workspace=$(pwd)
export NUM_JOBS=$(($(grep ^processor /proc/cpuinfo | wc -l)*2))
export USE_CCACHE=1
export CCACHE_DIR=~/mydroid/.ccache
${workspace}/prebuilts/misc/linux-x86/ccache/ccache -M 50G
. ./build/envsetup.sh
lunch orangepi_plus2e-userdebug
make -j${NUM_JOBS} 2>&1 | tee ../android_build.log
```
