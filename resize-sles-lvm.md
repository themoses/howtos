# How to extend a SLES 12/15 disk using LVM

## Resize the virtual disk

In my case I resized the virtual disk of the server in vCenter from 40GiB to 60GiB

## Resize the partition

To have a look at the partition table you can use `fdisk -l` and it should indicate the virtual disk size

```bash
fdisk -l
Disk /dev/sda: 60 GiB, 64424509440 bytes, 125829120 sectors
...
```

### Rescan the device

If the new size does not show up properly, use `echo 1 > /sys/block/sda/device/rescan`

Now we can use `parted` to extend the LVM partition - in my case /dev/sda2

```bash
parted /dev/sda
(parted) resize 2 60GB # use the partition number for your partition here
Ignore/Cancel? i
(parted)q(uit)
```

Usually this should be enough, but to force the partition update to the kernel we need to use `partx`

### Report partition change

```bash
partx -u -n 2 /dev/sda
```

## Resize LVM

### Resize the PV

LVM brings everything with it to manage the resizing of PVS with `pvresize`

```bash
pvresize /dev/sda2
```

### Extend the LV

To extend the Logical Volume to its maximal size, use `lvextend`

```bash
lvextend -l +100%FREE /dev/VOLGROUPNAME/LOGVOLNAME # find out about this with vgs and lvs
lvextend -lr +100%FREE /dev/VOLGROUPNAME/LOGVOLNAME # to extend the filesystem in one go and skip the next step
```

## Extend the filesystem

Use whatever tool your FS offers you

### BTRFS

```bash
btrfs filesystem resize max /
```

### XFS

```bash
xfs_growfs /
```

Check the new size of your filesystem with `df -hT`
