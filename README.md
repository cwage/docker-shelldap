# Docker image for [Shelldap](http://projects.martini.nu/shelldap/)

Based on [Alpine Linux](http://alpinelinux.org/).

## Description

From the Shelldap README:

A handy shell-like interface for browsing LDAP servers and editing their
content. It keeps command history, has sane autocompletes, credential caching,
site-wide and individual configs, and it's fun to say.
Shelldap! Shelldap! Shelldap!

Witness!

```
% shelldap 
~ > [ tab ]
~ > 
cat     clear   cp      delete  env     grep    id      ls      move    passwd  read    search  touch   whoami  
cd      copy    create  edit    exit    help    list    mkdir   mv      pwd     rm      setenv  vi      
~ > cd ou=People
ou=People,~ > cat uid=ma[ tab ]
ou=People,~ > cat uid=mahlon

dn: uid=mahlon,ou=People,dc=laika,dc=com
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
objectClass: posixAccount
objectClass: shadowAccount
objectClass: apple-user
cn: Mahlon E. Smith
departmentNumber: Technology - IT
displayName: Mahlon
gecos: Mahlon E. Smith
gidNumber: 200
givenName: Mahlon
homeDirectory: /home/m/mahlon
l: Ghetto
loginShell: /bin/tcsh
mail: mahlon@martini.nu
mobile: 1+8829999005747
sn: Smith
title: Manager, Information Systems
uid: mahlon
uidNumber: 20933
userPassword: *

ou=People,~ > 
```

## Usage

	docker run --rm -ti cwage/shelldap --server ldap://server:389 --binddn cn=root

If you would like to keep your history and server settings, just use a volume (with Docker >= 1.10):

	docker run --rm -ti -v my-shelldap-settings:/root cwage/shelldap --server ldap://server:389 --binddn cn=root

You can even use a different volume for each LDAP server you connect to, if you want to keep your history and settings separate.

Remember that you might need to use SSH tunnels to get access to your LDAP server...
