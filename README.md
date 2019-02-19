# ADIT manifest for RCAR-3 Android

This version is based on Android 9.0.0 [Release 30 (PQ1A.190105.004)](https://android.googlesource.com/platform/manifest/+/refs/heads/android-9.0.0_r30/default.xml).

## Fetching Android sources
```bash
mkdir -p ${ANDROID_ROOT}
cd ${ANDROID_ROOT}/
```

### HTTPS
```bash
repo init -u https://github.com/android2orangepi-dev/android_allwinner_manifest -b android-allwinner
repo sync -j1
```
