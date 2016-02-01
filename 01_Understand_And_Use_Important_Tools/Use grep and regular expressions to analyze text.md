### Use grep and regular expressions to analyze text
---

- Check file for commented out lines: `grep ‘^#’ <file>`
	```
	[root@centos ~]# grep '^#' grep_me
	# This is a comment
	```
- Check file for uncommented out lines: `grep -v ‘^#’ <file>`
	```
	[root@centos ~]# grep -v '^#' grep_me
	conf_setting=true
	```
- Check file for a particular line: `grep -i '^<line>$’ <file>`
	```
	[root@centos ~]# grep -i '^conf_setting=true$' grep_me
	conf_setting=true
	[root@centos ~]# grep -i '^conf_setting=tru$' grep_me
	[root@centos ~]#
	```

