### Refer
https://deepwiki.com/linux-sunxi/meta-sunxi/8-build-guide

### NoteNote
```
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