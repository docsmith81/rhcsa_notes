### Create and remove physical volumes, assign physical volumes to volume groups, and create and delete logical volumes
---
aka how to LVM

List current storage with `lsblk`:
```
[root@centos-server ~]# lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0   15G  0 disk
├─sda1   8:1    0    1G  0 part [SWAP]
└─sda2   8:2    0   10G  0 part /
sdb      8:16   0    2G  0 disk
sdc      8:32   0    2G  0 disk
sdd      8:48   0    2G  0 disk
sde      8:64   0    2G  0 disk
sdf      8:80   0    2G  0 disk
sr0     11:0    1 1024M  0 rom
```

##### Physical Volumes

`pvcreate /dev/sdb`: creates physical volume

`pvremove /dev/sdb`: removes physical volume

`pvs`: lists physical volumes

##### Volume Groups

`vgcreate -s 16m vg01 /dev/sdb`: creates volume group

`vgextend vg01 /dev/sdc`: extends volume group using new physical volume

`vgreduce vg01 /dev/sdc`: reduces volume group by removing listed physical volume

`vgremove vg01`: removed existing volume group

`vgs`: lists volume groups

##### Logical Volumes

`lvcreate --size 1G --name lv_volume vg01`: creates 1GB logical volume from vg01

`lvremove /dev/vg01/lv_volume`: removes logical volume

`lvresize -L 2G -r /dev/vg01/lv_volume`: resize logical volume and filesystem (works for both growing and shrinking)

`lvs`: lists logical volumes