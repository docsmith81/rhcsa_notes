### List, create, delete partitions on MBR and GPT disks
---

Verify added disks using `lsblk`:
```
[root@centos-server ~]# lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0   15G  0 disk
├─sda1   8:1    0    1G  0 part [SWAP]
└─sda2   8:2    0   10G  0 part /
sdb      8:16   0    2G  0 disk
sdc      8:32   0    2G  0 disk
sdd      8:48   0    2G  0 disk
sr0     11:0    1 1024M  0 rom
```

##### MBR
Create MBR partitions with `parted`:
```
root@centos-server ~]# parted /dev/sdf
GNU Parted 3.1
Using /dev/sdf
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) print
Error: /dev/sdf: unrecognised disk label
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdf: 2147MB
Sector size (logical/physical): 512B/512B
Partition Table: unknown
Disk Flags:
(parted) mklabel msdos
(parted) mkpart primary 1 2G
(parted) print
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdf: 2147MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags:

Number  Start   End     Size    Type     File system  Flags
 1      1049kB  2147MB  2146MB  primary
```

Delete MBR partitions with `parted`:
```
[root@centos-server ~]# parted /dev/sdf
GNU Parted 3.1
Using /dev/sdf
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) print
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdf: 2147MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags:

Number  Start   End     Size    Type     File system  Flags
 1      1049kB  2147MB  2146MB  primary

(parted) rm 1
(parted) print
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdf: 2147MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags:

Number  Start  End  Size  Type  File system  Flags

(parted) quit
Information: You may need to update /etc/fstab.
```

##### GPT
Create GPT partitions with `gdisk`:
```
[root@centos-server ~]# gdisk /dev/sdf
GPT fdisk (gdisk) version 0.8.6

Partition table scan:
  MBR: not present
  BSD: not present
  APM: not present
  GPT: not present

Creating new GPT entries.

Command (? for help): o
This option deletes all partitions and creates a new protective MBR.
Proceed? (Y/N): y

Command (? for help): p
Disk /dev/sdf: 4194304 sectors, 2.0 GiB
Logical sector size: 512 bytes
Disk identifier (GUID): 0AB2D9E1-4511-42C9-9A08-F8D9DE12BD4D
Partition table holds up to 128 entries
First usable sector is 34, last usable sector is 4194270
Partitions will be aligned on 2048-sector boundaries
Total free space is 4194237 sectors (2.0 GiB)

Number  Start (sector)    End (sector)  Size       Code  Name

Command (? for help): n
Partition number (1-128, default 1):
First sector (34-4194270, default = 2048) or {+-}size{KMGTP}:
Last sector (2048-4194270, default = 4194270) or {+-}size{KMGTP}:
Current type is 'Linux filesystem'
Hex code or GUID (L to show codes, Enter = 8300):
Changed type of partition to 'Linux filesystem'

Command (? for help): p
Disk /dev/sdf: 4194304 sectors, 2.0 GiB
Logical sector size: 512 bytes
Disk identifier (GUID): 0AB2D9E1-4511-42C9-9A08-F8D9DE12BD4D
Partition table holds up to 128 entries
First usable sector is 34, last usable sector is 4194270
Partitions will be aligned on 2048-sector boundaries
Total free space is 2014 sectors (1007.0 KiB)

Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048         4194270   2.0 GiB     8300  Linux filesystem

Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): y
OK; writing new GUID partition table (GPT) to /dev/sdf.
The operation has completed successfully.
```

Delete GPT partitions using `gdisk`:
```
[root@centos-server ~]# gdisk /dev/sdf
GPT fdisk (gdisk) version 0.8.6

Partition table scan:
  MBR: protective
  BSD: not present
  APM: not present
  GPT: present

Found valid GPT with protective MBR; using GPT.

Command (? for help): p
Disk /dev/sdf: 4194304 sectors, 2.0 GiB
Logical sector size: 512 bytes
Disk identifier (GUID): 0AB2D9E1-4511-42C9-9A08-F8D9DE12BD4D
Partition table holds up to 128 entries
First usable sector is 34, last usable sector is 4194270
Partitions will be aligned on 2048-sector boundaries
Total free space is 2014 sectors (1007.0 KiB)

Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048         4194270   2.0 GiB     8300  Linux filesystem

Command (? for help): d1
Using 1

Command (? for help): p
Disk /dev/sdf: 4194304 sectors, 2.0 GiB
Logical sector size: 512 bytes
Disk identifier (GUID): 0AB2D9E1-4511-42C9-9A08-F8D9DE12BD4D
Partition table holds up to 128 entries
First usable sector is 34, last usable sector is 4194270
Partitions will be aligned on 2048-sector boundaries
Total free space is 4194237 sectors (2.0 GiB)

Number  Start (sector)    End (sector)  Size       Code  Name

Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): y
OK; writing new GUID partition table (GPT) to /dev/sdf.
The operation has completed successfully.
```