### Access remote systems using ssh
---

Accessing hosts:
```
#  ssh <user>@<hostname or IP>
```

```
#  ssh slapula@random-host.com
Password:
```

Relevent Files:
```
Config Files
/etc/ssh/ssh_config
/etc/ssh/sshd_config

SSH Keys
~/.ssh/known_hosts
```

Executing remote commands via SSH:
```
[root@centos ~]# ssh user@54.152.93.214 ls -lah
user@54.152.93.214's password:
total 52K
drwx------.  8 user user 4.0K Feb  1 18:10 .
drwxr-xr-x.  3 root root   17 Aug 12 14:22 ..
-rw-r--r--.  1 user user    9 Feb  1 18:14 .bash_history
-rw-r--r--.  1 user user   18 Jan 27 16:56 .bash_logout
-rw-r--r--.  1 user user  193 Jan 27 16:56 .bash_profile
-rw-r--r--.  1 user user  231 Jan 27 16:56 .bashrc
drwx------.  6 user user 4.0K Dec 19 23:02 .cache
drwxr-xr-x. 11 user user 4.0K Aug  6 19:50 .config
drwxr-xr-x.  2 user user    6 Jan  7  2015 Desktop
-rw-------.  1 user user   16 Jan 27 16:56 .esd_auth
-rw-------.  1 user user 3.4K Jan 27 16:56 .ICEauthority
drwxr-xr-x.  3 user user   18 Jan  7  2015 .local
drwxrwxr-x.  3 user user   14 Jan 12  2015 .openoffice
-rw-------.  1 user user  891 Jan 27 16:56 .viminfo
drwxrwxr-x.  2 user user 4.0K Feb  1 18:10 .vnc
-rw-rw-r--.  1 user user  431 Aug  6 19:48 VNCHOWTO
-rw-------.  1 user user 1.1K Feb  1 18:10 .Xauthority
```

Copying files via SCP:
```
[root@centos ~]# scp grep_me user@54.152.93.214:/home/user/
user@54.152.93.214's password:
grep_me                                                                                                            100%   38     0.0KB/s   00:00
[root@centos ~]# ssh user@54.152.93.214 ls /home/user
user@54.152.93.214's password:
Desktop
grep_me
VNCHOWTO
```