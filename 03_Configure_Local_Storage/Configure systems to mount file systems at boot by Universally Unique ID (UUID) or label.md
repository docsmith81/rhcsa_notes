### Configure systems to mount file systems at boot by Universally Unique ID (UUID) or label
---


##### Mounting with UUID

`blkid` to get a list of disk UUIDs:
```
[root@centos-server ~]$ blkid
/dev/sde: UUID="dN4E1f-GEW1-AFbe-GBaO-KOC8-0YeP-M12qwL" TYPE="LVM2_member"
/dev/sdd: UUID="63qDI5-YmLD-VxYk-ouVZ-Eebb-MDCz-UPklXc" TYPE="LVM2_member"
/dev/sdb: UUID="ELmb1V-JYmp-gkl0-4dxg-GZmu-Tvdr-GtUd7B" TYPE="LVM2_member"
/dev/sda1: UUID="92cbe45f-dccb-449a-9e3d-d573e1a5ee7e" TYPE="swap"
/dev/sda2: UUID="80b06365-6b27-4f63-8b1d-76bfe160a01b" TYPE="ext4"
/dev/sdc: UUID="mjm3df-p1q6-uXwH-t2x5-BDQx-oFD3-H8Uhk7" TYPE="LVM2_member"
```

Edit `/etc/fstab` to add disk/partition to system:
```
UUID=80b06365-6b27-4f63-8b1d-76bfe160a01b		/blah 		ext4 defaults 	1 2
```

Mount disk/partition with `mount /blah`

##### Mounting with Label

Label a partition with `e2label /dev/sdb1 blah`

`e2label /dev/sdb1` will return the label for said partition

Edit `/etc/fstab` to add disk/partition to system:
```
LABEL=blah		/blah 		ext4 defaults 	1 2
```

Mount disk/partition with `mount /blah`