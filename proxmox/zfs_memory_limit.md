As a general rule of thumb, allocate at least **2 GiB Base + 1 GiB/TiB**-Storage
```bash
echo "$[3 * 1024*1024*1024 - 1]" > /sys/module/zfs/parameters/zfs_arc_min
echo "$[3 * 1024*1024*1024]" > /sys/module/zfs/parameters/zfs_arc_max
```

To permanently change the ARC limits, add the following line to `/etc/modprobe.d/zfs.conf`:  
  
**3 GiB**: 3221225472
```bash
options zfs zfs_arc_max=3221225472
options zfs zfs_arc_min=3221225471
```

**5 GiB**: 5368709120
```bash
options zfs zfs_arc_max=5368709120
options zfs zfs_arc_min=5368709119
```

**8 GiB**: 8589934592
```bash
options zfs zfs_arc_max=8589934592
options zfs zfs_arc_min=8589934591
```

**10 GiB**: 1099511627776
```bash
options zfs zfs_arc_max=1099511627776
options zfs zfs_arc_min=1099511627775
```
