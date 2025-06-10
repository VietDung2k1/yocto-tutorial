### Refer
https://deepwiki.com/linux-sunxi/meta-sunxi/8-build-guide

### Note
```
sudo apt install zstd
Branch kirkstone

sgtpc@sgtpc-X99E:~/Workspace/yocto-opiz/build/conf$ cat bblayers.conf 
# POKY_BBLAYERS_CONF_VERSION is increased each time build/conf/bblayers.conf
# changes incompatibly
POKY_BBLAYERS_CONF_VERSION = "2"

BBPATH = "${TOPDIR}"
BBFILES ?= ""

BBLAYERS ?= " \
    ...
  /home/sgtpc/Workspace/yocto-opiz/meta-arm/meta-arm-toolchain \
  /home/sgtpc/Workspace/yocto-opiz/meta-arm/meta-arm \
  /home/sgtpc/Workspace/yocto-opiz/meta-arm/meta-arm-bsp \
  "
```
### Add Thingsboard gateway and Tailscale
```
Thingsboard Gateway - Requires meta-oe, meta-python
Add line in local.conf
IMAGE_INSTALL += " thingsboard-gateway"

Tailscale
git clone https://github.com/ChristophHandschuh/meta-tailscale.git
bitbake-layers add-layer ../meta-tailscale
Add line in local.conf
IMAGE_INSTALL += " tailscale"
```