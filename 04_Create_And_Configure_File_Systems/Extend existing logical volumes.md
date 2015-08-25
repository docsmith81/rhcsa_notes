### Extend existing logical volumes
---

Use `vgdisplay` and `lvdisplay` to determine if/how you can expand logical volume:

```
[root@centos-server ~]# vgdisplay
  --- Volume group ---
  VG Name               vg-test
  System ID
  Format                lvm2
  Metadata Areas        3
  Metadata Sequence No  2
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                1
  Open LV               0
  Max PV                0
  Cur PV                3
  Act PV                3
  VG Size               5.91 GiB
  PE Size               48.00 MiB
  Total PE              126
  Alloc PE / Size       43 / 2.02 GiB
  Free  PE / Size       83 / 3.89 GiB
  VG UUID               AEalxW-BcfZ-tzU9-JIwD-3IA1-MD3s-fBnSqT

[root@centos-server ~]# lvdisplay
  --- Logical volume ---
  LV Path                /dev/vg-test/lv-test
  LV Name                lv-test
  VG Name                vg-test
  LV UUID                Feb8I4-g2Y7-PBH9-sarU-KP7Y-K00Y-x8L4lu
  LV Write Access        read/write
  LV Creation host, time centos-server, 2015-08-17 00:44:48 -0400
  LV Status              available
  # open                 0
  LV Size                2.02 GiB
  Current LE             43
  Segments               2
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:0
```

Extend logical volume (-r will resize the filesystem):
```
[root@centos-server ~]# lvextend -L +3G -r /dev/vg-test/lv-test
fsck from util-linux 2.23.2
/dev/mapper/vg--test-lv--test: clean, 11/132192 files, 26240/528384 blocks
  Size of logical volume vg-test/lv-test changed from 2.02 GiB (43 extents) to 5.02 GiB (107 extents).
  Logical volume lv-test successfully resized
resize2fs 1.42.9 (28-Dec-2013)
Resizing the filesystem on /dev/mapper/vg--test-lv--test to 1314816 (4k) blocks.
The filesystem on /dev/mapper/vg--test-lv--test is now 1314816 blocks long.
```

Reduce logical volume (again -r will resize the filesystem):
```
[root@centos-server ~]# lvresize -L 2G -r /dev/vg-test/lv-test
  Rounding size to boundary between physical extents: 2.02 GiB
fsck from util-linux 2.23.2
/dev/mapper/vg--test-lv--test: clean, 11/318816 files, 38470/1314816 blocks
resize2fs 1.42.9 (28-Dec-2013)
Resizing the filesystem on /dev/mapper/vg--test-lv--test to 528384 (4k) blocks.
The filesystem on /dev/mapper/vg--test-lv--test is now 528384 blocks long.

  Size of logical volume vg-test/lv-test changed from 5.02 GiB (107 extents) to 2.02 GiB (43 extents).
  Logical volume lv-test successfully resized
```

##### XFS notes

XFS cannot be reduced using the method above. You will need to back it up and recreate the partition with the desired size.

`lvextend` with -r will also resize the filesystem automatically for you. Nice.