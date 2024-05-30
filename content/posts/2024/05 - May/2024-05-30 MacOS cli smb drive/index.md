---
title: "CLI Mount/Unmount SMB Network Volume"
date: "2024-05-30"
categories: ["NAS"]
---

## SMBUTIL

You can reveal the staus of the network drive via `smbutil status $IP_or_Domain` command:

```
> smbutil status example.com
> STDOUT:
>   Using IP address of example.com: XXX.XXX.XXX.XXX
>   Workgroup: WORKGROUP
>   Server: XXXXXXX
```

You can reveal the drive available via `smbutil view -A //$usr@$ip` (or with password `smbutil view -A //$usr:$pwd@$ip`), you will need to run the command once to authenticate, and another time to reveal the available volumes:

```
> smbutil view -A //suowei.h@XXX.XXX.XXX.XXX
> STDOUT:
    Please Enter password for suowei.h: *********************
    Authenticate successfully with //suowei.h@XXX.XXX.XXX.XXX
> 
> smbutil view -A //suowei.h@XXX.XXX.XXX.XXX
> STDOUT
    Share Type  Comments
    ----- ----  ---------------------------------
    XXXX  Disk  Western Digital Technologies, Inc.
    XXXX  Disk  Western Digital Technologies, Inc.
    XXXX  Disk  Western Digital Technologies, Inc.
    XXXX  Disk  Western Digital Technologies, Inc.
    XXXX  Disk  Western Digital Technologies, Inc.
    XXXX  Disk  Home directory of suowei.h
    XXXX  Disk  Western Digital Technologies, Inc.
    XXXX  Disk  Western Digital Technologies, Inc.
    XXXX  Disk  System default shared folder
    IPC$  Pipe  IPC Service ()
    10 shares listed
```



## SMBCLIENT

### Preliminary Requirement: Install Samba
**Samba** is a free software re-implementation of the **SMB networking protocol**, and provides file and print services across multiple operating systems including Linux, Unix, and Windows. **Smbclient** is a command-line tool included in the Samba suite. It functions somewhat like an FTP client and allows users to connect to an SMB/CIFS (Common Internet File System) server. 

Consequently we'll install Samba first: 

- For MacOS device: `brew install samba`

- For Linux device: `yum -y install samba samba-client samba-common`

-   For Windows device: https://www.liquidweb.com/kb/how-to-install-samba-on-linux-windows/

### 