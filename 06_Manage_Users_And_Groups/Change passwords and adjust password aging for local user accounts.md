Change passwords and adjust password aging for local user accounts

Display password aging information on user:
# chage --list <username>

Change password after maximum amount of days:
# chage -M 120 <username>

Change password every X amount of days:
# chage -m 120 <username>

Force user to change password on next login:

# chage -m 0 <username>