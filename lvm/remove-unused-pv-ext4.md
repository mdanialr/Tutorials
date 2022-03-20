# Remove '__unused__' PV (`Ext4` FS only)

## Unmount the file system
```
sudo umount /mount/point/of/the/LV_path
```

## Check the file system for any Errors
```
sudo e2fsck -f /LV_path
```

## Shrink the FS. maybe to 5G
```
sudo resize2fs /LV_path 5G
```

## Reduce LV size. maybe to 5G
```
sudo lvreduce -L 5G /LV_path
```

## ReCheck any FS errors
```
sudo e2fsck -f /LV_path
```

## Remount the already shrinked FS
```
sudo mount /LV_path /mount/point/name
```

## Make sure PV not used
if in tab 'Used' the size is 0 then you are good to go.
```
sudo pvs -o+pv_used
```

## Remove PV from VG
```
sudo vgreduce the-vg-name /dev/sdXX
```

## Remove PV from LVM
```
sudo pvremove /dev/sdXX
```
Finally, you are good to remove the disk

## Make sure the physical disk is no longer labaled as LVM
```
sudo lvmdiskscan
```
