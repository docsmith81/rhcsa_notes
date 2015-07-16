### Interrupt the boot process in order to gain access to a system
---

1. Interrupt Grub2 boot process. Select the kernel you are going to access  and press `e`.
2. Go to the kernel line. Remove `rhgb quiet` and add `init=/bin/sh`. Continue booting by pressing `CTRL+X`
3. When the prompt appears, execute `/usr/sbin/load_policy -i` to load the SELinux security policy.
4. Remount the root partition like so `mount -o remount,rw /`.
5. If you need to change the root password you can do so now by executing `passwd`.
6. Remount the root partition again to make read-only `mount -o remount,ro /`.
7. Restart the host with `exec /sbin/init`