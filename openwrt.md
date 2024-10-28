# OpenWrt on BPi-R4

**Download OpenWrt**

```bash
curl -vo openwrt_snapshot_bpi-r4-sd.img.gz https://downloads.openwrt.org/snapshots//targets/mediatek/filogic/openwrt-mediatek-filogic-bananapi_bpi-r4-sdcard.img.gz
```

**Zero the sd card**

```bash
dd if=/dev/zero of=/dev/mmcblk0 bs=4096 status=progress
# Might run into error when size of sd card is not a multiple of the block size 'bs'
```

**Write image to sd card**

```bash
zcat openwrt_snapshot_bpi-r4-sd.img.gz | sudo dd of=/dev/mmcblk0 bs=1M status=progress
```