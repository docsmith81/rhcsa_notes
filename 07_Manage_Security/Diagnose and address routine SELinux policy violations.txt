Diagnose and address routine SELinux policy violations

SElinux logs messages to /var/log/audit/audit.log and will be labeled avc.

SELinux Troubleshooter GUI
# sealert -b

SELinux Troubleshooter using cmd line:
# sealert -l *

Make use logging services are running:
# service rsyslog status

# service auditd stat