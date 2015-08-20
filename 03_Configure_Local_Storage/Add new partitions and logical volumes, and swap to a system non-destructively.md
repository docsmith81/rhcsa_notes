### Add new partitions and logical volumes, and swap to a system non-destructively
---

##### Swap via Partition Configuration

1. Create new partition:
```
root@centos-server ~]# parted /dev/sdf
GNU Parted 3.1
Using /dev/sdf
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) mklabel
New disk label type? gpt
Warning: The existing disk label on /dev/sdf will be destroyed and all data on this disk will be lost. Do you want to continue?
Yes/No? yes
(parted) mkpart
Partition name?  []? new_part
File system type?  [ext2]? ext4
Start? 1
End? 2GB
(parted) p
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdf: 2147MB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags:

Number  Start   End     Size    File system  Name      Flags
 1      1049kB  2146MB  2145MB               new_part

(parted) quit
```

2. Format partition for swap with `mkswap /dev/sdf1`

3. Enable system to use the new partion as swap with `swapon /dev/sdf1`

4. Verify swap partitions:
```
[root@centos-server ~]# swapon -s
Filename				Type		Size	Used	Priority
/dev/sda1                              	partition	1048572	20884	-1
/dev/sdf1                              	partition	2095100	0	-2
```

5. Add line to `/etc/fstab` to make new swap partition persistant on reboot:
```
/dev/sdf1 	swap 	swap 	defaults 	0 0
```

Deactivate new swap partition using `swapoff /dev/sdf1`

##### Swap via LVM

1. Create physical volume with `pvcreate /dev/sdf`

2. Extend volume group to include new partition with `vgextend vg01 /dev/sdf`

3. Create swap logical volume with `lvcreate --size 2G --name lv_swap vg01`

4. Enable system to use swap logical volume with `swapon /dev/vg01/lv_swap`

5. Verify swap partitions with `swapon -s`

6. Add line to `/etc/fstab` to make new swap partition persistant on reboot:
```
/dev/mapper/vg01-lv_swap 	swap 	swap 	defaults 	0 0
```

Deactivate new swap partition using `swapoff /dev/vg01/lv_swap` then remove the logical volume with `lvremove /dev/vg01/lv_swap`