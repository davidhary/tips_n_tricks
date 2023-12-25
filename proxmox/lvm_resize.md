# Proxmox LVE optimize

## Remove data logical volume
```bash
lvremove /dev/pve/data
```

## Extend root volume to 100%
```bash
lvextend -l 100%FREE /dev/pve/root
```

## Resize root volume to 100%
```bash
resize2fs /dev/pve/root
xfs_growfs /dev/pve/root
```

---

# Backup drive optimize
Mount the drive

Edit `/etc/pve/storage.cfg`
```
dir: backup
        path /mnt/backup
        content snippets,backup,iso,rootdir,images,vztmpl
```		

Modify `/etc/fstab`
