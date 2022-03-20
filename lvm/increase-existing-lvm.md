# Increase LVM size (One existing Disk then add another new Disk)
![LVM images](https://user-images.githubusercontent.com/48054961/159128814-a58e429d-3c8c-4373-a366-8e39cde68eea.png)
## Display PV (Physical Volume)
```
sudo pvs
```
or more detailed
```
sudo pvdisplay
```

## Display VG (Volume Group)
```
sudo vgs
```
or more detailed
```
sudo vgdisplay
```

## Display LV (Logical Volume)
```
sudo lvs
```
or more detailed
```
sudo lvdisplay
```

## Scan new added Disk
```
sudo lvmdiskscan
```

## Create PV on new Disk
```
sudo pvcreate /dev/vdXX
```
then rescan again using `sudo lvmdiskscan -l` to show only LVM devices.

## Extend newly created PV to existing VG
```
sudo vgextend name-of-the-vg /dev/vdXX
```

## Extend existing target LV from just now extended VG
give all remaining free size of the VG
```
sudo lvextend -l +100%FREE /dev/name-of/the-lv
```
or just some size maybe 10GB using
```
sudo lvextend -L+10G /dev/name-of/the-lv
```

## Resize just now extended LV
```
sudo xfs_growfs /dev/name-of/the-lv
```
or if using `ext4` filesystem use this instead
```
sudo resize2fs /dev/name-of/the-lv
```

## Check the new size
```
df -h
```
and
```
sudo lvdisplay
```
