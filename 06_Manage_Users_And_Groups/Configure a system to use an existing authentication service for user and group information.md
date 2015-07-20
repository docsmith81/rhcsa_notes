### Configure a system to use an existing authentication service for user and group information
---
Make sure LDAP packages are installed:
```
yum -y install openldap openldap-clients authconfig nss-pam-ldapd sssd
```

##### Graphical Configuration
`authconfig-tui`: Configure exsisting LDAP directory with TUI

Or

`authconfig-gtk`: Configure exsisting LDAP directory with GUI

##### Command Line Configuration
1. Configure LDAP client to use LDAP server: `authconfig --enableldap --enableldapauth --ldapserver=ldap://server.example.com --enablesssd --ldapbasedn="dc=example,dc=com" --update`
2. Confirm the settings are correct in the `sssd` configuration files `/etc/sssd/sssd.conf` and `/etc/openldap/ldap.conf`