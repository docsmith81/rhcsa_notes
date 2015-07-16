Create, delete, and modify local user accounts

Create users with GUI:
# system-config-users

Add user:
# useradd joe

Add user to group:
# useradd -G group1 joe

Add sh to user account:
# useradd -s /bin/sh joe

Set UID and GID for user:
# useradd -u 504 -g  505 joe

Add additional group to user:
# useradd -a -G group2 joe

Change user password:
# passwd joe

Delete user:
# userdel joe

Force delete user (even if he/she is logged in):

# userdel -f joe