## Ubuntu 20.04 WSL
### Enviroment
```
sudo apt-get install git cmake vim autoconf -y
sudo apt-get install python-minimal -y
sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib build-essential chrpath socat libsdl1.2-dev xterm -y
sudo apt-get install libcurl-ocaml-dev libmosquitto-dev libmosquittopp-dev libusb-1.0-0-dev libssl-ocaml-dev -y
sudo apt-get install bison flex swig libtool curl -y
sudo apt-get install uuid-dev libacl1-dev liblzo2-dev libzstd-dev lib32z1 device-tree-compiler minicom -y
sudo apt-get install libncurses5-dev libncursesw5-dev -y
sudo apt-get install cpio python2 python2.7 python-dev -y
```
### Clone source
```
git clone git://git.yoctoproject.org/poky --depth 1 -b dunfell
git clone git://git.openembedded.org/meta-openembedded --depth 1 -b dunfell
git clone https://github.com/meta-qt5/meta-qt5.git --depth 1 -b dunfell
git clone https://github.com/voloviq/meta-licheepinano --depth 1 -b dunfell
``` 
### Add bblayes 
```
bitbake-layers add-layer ../meta-openembedded/meta-oe
bitbake-layers add-layer ../meta-openembedded/meta-python
bitbake-layers add-layer ../meta-openembedded/meta-networking
bitbake-layers add-layer ../meta-qt5
bitbake-layers add-layer ../meta-licheepinano
```
### Local config
```
MACHINE ??= "licheepinano-sdcard"

CONF_VERSION = "1"

RM_OLD_IMAGE = "1"
INHERIT += "rm_work"

#QT
QT_DEV_TOOLS = " \
qtbase-dev \
qtbase-mkspecs \
qtbase-tools \
qtserialport-dev \
qtserialport-mkspecs \
qtdeclarative \
qtdeclarative-qmlplugins \
qttranslations-qtdeclarative \
qtmultimedia \
qtmultimedia-plugins \
qtsvg \
qtsvg-plugins \
qtsensors \
qtimageformats-plugins \
qtsystems \
qtsystems-tools \
qtsystems-qmlplugins \
qtscript \
qtconnectivity-dev \
qtconnectivity-mkspecs \
qtconnectivity-qmlplugins \
qtlocation-plugins \
qtlocation-qmlplugins \
qtquickcontrols-qmlplugins \
qtxmlpatterns-dev \
qtxmlpatterns-mkspecs \
qttranslations-qtxmlpatterns \
qtquickcontrols2 \
qtquickcontrols2-dev \
qtquickcontrols2-mkspecs \
qtcharts \
"

QT_TOOLS = " \
    qtbase \
    qtbase-plugins \
    qtserialport \
    qt5-env \
"
FONTS = " \
    fontconfig \
    fontconfig-utils \
    ttf-bitstream-vera \
"

TSLIB = " \
    tslib \
    tslib-calibrate \
    tslib-conf \
"

CORE_OS = " \
    packagegroup-core-boot \
    tzdata \
"

KERNEL_EXTRA_INSTALL = " \
    kernel-modules \
"

WIFI_SUPPORT = " \
    crda \
    iw \
    linux-firmware-ath9k \
    linux-firmware-ralink \
    linux-firmware-rtl8192ce \
    linux-firmware-rtl8192cu \
    linux-firmware-rtl8192su \
    linux-firmware-wl18xx \
    wpa-supplicant \
"

DEV_SDK_INSTALL = " \
    binutils \
    binutils-symlinks \
    coreutils \
    cpp \
    cpp-symlinks \
    diffutils \
    elfutils \
    file \
    g++ \
    g++-symlinks \
    gcc \
    gcc-symlinks \
    gdb \
    gettext \
    git \
    ldd \
    libstdc++ \
    libstdc++-dev \
    libtool \
    ltrace \
    make \
    nasm \
    perl-modules \
    pkgconfig \
    python3-modules \
    strace \
    mtd-utils \
    dbus \
"

DEV_EXTRAS = " \
    ntp \
    ntp-tickadj \
"

EXTRA_TOOLS_INSTALL = " \
    bzip2 \
    devmem2 \
    dosfstools \
    e2fsprogs-mke2fs \
    ethtool \
    findutils \
    i2c-tools \
    iperf3 \
    iproute2 \
    iptables \
    less \
    nano \
    netcat \
    parted \
    procps \
    sysfsutils \
    tcpdump \
    tree \
    unzip \
    util-linux \
    util-linux-blkid \
    wget \
    xz \
    zip \
    make \
    cmake \
"

IMAGE_INSTALL_append += " \
    ${QT_TOOLS} \
    ${CORE_OS} \
    ${DEV_SDK_INSTALL} \
    ${DEV_EXTRAS} \
    ${EXTRA_TOOLS_INSTALL} \
    ${KERNEL_EXTRA_INSTALL} \
    ${WIFI_SUPPORT} \
"

IMAGE_INSTALL_append += " \
    ${FONTS} \
    ${QT_TOOLS} \
    ${QT_DEV_TOOLS} \
    ${TSLIB} \
"
```
### Build and Flash
```
bitbake core-image-minimal
bitbake console-image
bitbake qt5-image
bitbake meta-toolchain-qt5

sudo mkfs.ext4 /dev/sde

sudo dd if=qt5-image-licheepinano-sdcard.sunxi-sdimg of=/dev/sde bs=1024 status=progress
```