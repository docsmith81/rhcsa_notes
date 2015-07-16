Set enforcing and permissive modes for SELinux

Use setenforce to set the current running mode:
# setenforce permissive
# setenforce enforcing

Use getenforce to check current mode:
# getenforce


Edit /etc/selinux/config to configure default mode on startup