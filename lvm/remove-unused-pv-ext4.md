# Remove '__unused__' PV (`Ext4` FS only)

## Unmount the file system
```
sudo umount /dev/mapper/the-lv-name
```

## Check the file system for any Errors
```
sudo e2fsck -f /dev/mapper/the-lv-name
```

## Shrink the FS. maybe to 5G
```
sudo resize2fs /dev/mapper/the-lv-name 5G
```

## Reduce LV size. maybe to 5G
```
sudo lvreduce -L 5G /dev/mapper/the-lv-name
```

## ReCheck any FS errors
```
sudo e2fsck -f /dev/mapper/the-lv-name
```

## Remount the already shrinked FS
```
sudo mount /dev/mapper/the-lv-name
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
