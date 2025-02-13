# Using Ubuntu 20.04

# Install

```
sudo apt install autoconf bison build-essential cmake chrpath diffstat flex gawk git git-lfs lz4 python3-distutils python-is-python3 rsync zstd
```

# Install repo
```
sudo apt install repo
```

# Using Debian 10

# Install

```
sudo apt install autoconf bison build-essential cmake chrpath diffstat flex gawk git git-lfs lz4 python3-distutils repo rsync zstd
```

# Using Debian 11

# Install

```
sudo apt install autoconf bison build-essential cmake chrpath diffstat flex gawk git git-lfs lz4 python3-distutils python-is-python3 repo rsync zstd
```

# No Dash...
```
sudo dpkg-reconfigure dash
```

# Yocto

```
git clone --recurse-submodules -b Linux_SDK_V1.1.2-light-beagle https://github.com/beagleboard/xuantie-yocto.git xuantie-yocto ; cd ./xuantie-yocto
```

# Configure Build

```
source openembedded-core/oe-init-build-env thead-build/light-fm
```

# Build Options
```
You can now run 'bitbake <target>'

Common targets are:
    thead-image-gui
    thead-image-multimedia
    thead-image-linux
    thead-image-linux-test

machines:
    light-a-val
    light-beagle
    light-lpi4a
    light-b-product
```

# Copy mirrored downloads:

```
mkdir ../downloads ; rsync -av /mnt/yocto-cache/beaglev-ahead/Linux_SDK_V1.1.2/downloads/ ../downloads/
```

# Copy mirrored sstate-cache (assuming you built and saved sstate-cache in a prior build)

```
mkdir ../sstate-cache ; rsync -av /mnt/yocto-cache/beaglev-ahead/Linux_SDK_V1.1.2/sstate-cache/ ../sstate-cache/
```

# Download missing files:

```
BB_NUMBER_THREADS=4 MACHINE=light-beagle bitbake thead-image-linux --runall=fetch
rsync -av ../downloads/ /mnt/yocto-cache/beaglev-ahead/Linux_SDK_V1.1.2/downloads/ --delete
```

# Start Build

```
BB_NUMBER_THREADS=4 MACHINE=light-beagle bitbake -k thead-image-linux
```

# Save cache

```
rsync -av ../sstate-cache/ /mnt/yocto-cache/beaglev-ahead/Linux_SDK_V1.1.2/sstate-cache/ --delete
```
#

# Flashing Board

```
sudo fastboot flash ram ./tmp-glibc/deploy/images/light-beagle/u-boot-with-spl.bin
sudo fastboot reboot
sudo fastboot oem format
sudo fastboot flash uboot ./tmp-glibc/deploy/images/light-beagle/u-boot-with-spl.bin
sudo fastboot flash boot ./tmp-glibc/deploy/images/light-beagle/boot.ext4
sudo fastboot flash root ./tmp-glibc/deploy/images/light-beagle/thead-image-linux-light-beagle-*.rootfs.ext4
sudo fastboot reboot
```
#
