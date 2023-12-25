download link
releases / VERSION / targets / x86 / 64 / x86-64-generic-ext4-combined.img.gz
https://mirror-01.infra.openwrt.org/releases/23.05.2/targets/x86/64/

```bash
gunzip openwrt*
mv openwrt* openwrt.img
qemu-img resize -f raw ./openwrt.img 512M #optional
qm importdisk $VM_ID openwrt.img $DEST_STORAGE
```
