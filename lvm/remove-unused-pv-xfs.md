# Remove '__unused__' PV (`xfs` FS only)
Different with `EXT4` FS and `resize2fs`. `xfs` FS has no way to shrink or resize. So instead you need to reformat it to get new shrinked size
- backup to another PV first
- unmount partition
- reduce LV size
- reformat to `xfs` FS
- remount partition
- restore data back to partition
- remove PV from the associated VG
- remove PV from LVM

## Backup to another mount point
```
sudo xfsdump -f /target/path/to/backup /mount/point/name
```

## Unmount parition
```
sudo umount /mount/point/name
```

## Reduce LV size. maybe to 5G
```
sudo lvreduce -L 5G /LV_path
```

## Check new LV size & VG free size
see in tab 'Lsize'
```
sudo lvs
```
and see 'VFree'
```
sudo vgs
```

## Reformat the partition to xfs FS
```
sudo mkfs.xfs -f /LV_path
```

## Remount the partition
```
sudo mount /LV_path /mount/point/name
```

## Check newly shrinked partition size
```
df -h
```
and
```
sudo lvdisplay
```

## Restore data
```
sudo xfsrestore -f /target/path/to/backup /mount/point/name
```

## Remove PV from their associated VG
```
sudo vgreduce the-vg-name /dev/sdXX
```
Finally, you are good to remove the disk

## Remove PV from LVM
```
sudo pvremove /dev/sdXX
```

## Make sure the physical disk is no longer labaled as LVM
```
sudo lvmdiskscan
```
