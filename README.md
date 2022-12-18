# device-clamav
Provides a clam antivirus server appliance.

This appliance does the following:

- All parameters passed to the device commands are syntax checked and canonicalised, with bash completion.
- Automatically configures clamav's configuration files before startup.
- Binds securely to the unix domain socket /run/clamd.scan/clamd.sock.
- Autostarts when called for by other services like device-clamav-milter.
- Zero Trust configuration.

## before

- Deploy the device-clamav package.

```
[root@server ~]# dnf install device-clamav
```

## update virus database

To update the antivirus database now, run this.

```
[root@server ~]# device services antivirus update
ClamAV update process started at Sun Dec 18 16:30:58 2022
daily database available for update (local version: 26753, remote version: 26754)
Current database is 1 version behind.
Downloading database patch # 26754...
Time:    0.9s, ETA:    0.0s [========================>]   10.06KiB/10.06KiB
Testing database: '/var/lib/clamav/tmp.2f9f74b8b6/clamav-cc8ad91e9760967b1182da1624de05d8.tmp-daily.cld' ...
Database test passed.
daily.cld updated (version: 26754, sigs: 2014066, f-level: 90, builder: raynman)
main.cvd database is up-to-date (version: 62, sigs: 6647427, f-level: 90, builder: sigmgr)
bytecode.cvd database is up-to-date (version: 333, sigs: 92, f-level: 63, builder: awillia2)
```



# device-clamav-milter
Provides a clam antivirus milter appliance.

This appliance does the following:

- All parameters passed to the device commands are syntax checked and canonicalised, with bash completion.
- Automatically configures clamav milter's configuration files before startup.
- Binds securely to the unix domain socket /run/clamav-milter/clamav-milter.socket.
- Autostarts on server restart.
- Zero Trust configuration.

## before

- Deploy the device-clamav-milter package.

```
[root@server ~]# dnf install device-clamav-milter
```

## enable

To switch the appliance on, run this.

```
[root@server ~]# device services mail smtp antivirus enable 
```

## disable

To switch the appliance off, run this.

```
[root@server ~]# device services mail smtp antivirus disable  
```

