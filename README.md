# mkinitcpio-etc
This hook mounts a specified NFS path to /etc before the real `init` begins, primarily for diskless clients that share the same root file system but want different configurations. It's required to be used along with the "net" hook, and the last hook to run.

The hook accepts the following kernel parameter:

`etc=<server-ip>:<nfs-dir>`

The parameter can have these tokens:

`HOSTNAME` will be replaced by the hostname given by DHCP server or configured by `ip=` parameter.

`IPV4ADDR` will be replaced by the IPv4 address given by DHCP server or configured by `ip=` parameter.

`IPV4ADDRHEX` will be replaced by hexadecimal representation of the IPv4 address given by DHCP server or configured by `ip=` parameter.

e.g. The machine has the hostname "host0" and IP address 192.168.1.50, setting `etc=192.168.1.1:/srv/etc-HOSTNAME-IPV4ADDR-IPV4ADDRHEX` will make the hook attempt to mount `192.168.1.1:/srv/etc-host0-192.168.1.50-C0A80132` to `/etc`.