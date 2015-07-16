Create, delete, and modify local groups and group memberships

Display groups that include user:
# groupadd <username>

Add group:
# groupadd group1

Delete group:
# groupdel group1

Change group name:
# groupmod -n newgroup group1

Change group's GID:
# groupmod -g 507 group1

Add user to group:

# groupmems -g group1 -a <username>