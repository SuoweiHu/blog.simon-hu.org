---
title: "List/Mount/Unmount SMB Drive on CLI"
description: "List/Mount/Unmount network drive via cli"
date: "2024-05-30"
tags: ["NAS"]
---



## List Network Volume

### SMBUTIL

You can reveal the staus of the network drive (SMB volumes) via `smbutil status $IP_or_Domain` command:

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

### SMBCLIENT

#### Preliminary Requirement
**Samba** is a free software re-implementation of the **SMB networking protocol**, and provides file and print services across multiple operating systems including Linux, Unix, and Windows. **Smbclient** is a command-line tool included in the Samba suite. It functions somewhat like an FTP client and allows users to connect to an SMB/CIFS (Common Internet File System) server.

Consequently we'll install Samba first:

- For MacOS device: `brew install samba`

- For Linux device: `yum -y install samba samba-client samba-common`

-   For Windows device: https://www.liquidweb.com/kb/how-to-install-samba-on-linux-windows/

#### Usage

You can reveal the available volumes on the IP/Domain via command: `smbclient -L //${ip} --grepable --user=${usr} --password=${pwd} --workgroup=WORKGROUP`

```
> smbclient -L //XXX.XXX.XXX.XXX --grepable --user=suowei.h --password=********* --workgroup=WORKGROUP
> STDOUT
    Disk|外置硬盘①号|Western Digital Technologies, Inc.
    Disk|外置硬盘②号|Western Digital Technologies, Inc.
    Disk|🎓 笔记备份｜澳国立大学|
    Disk|🎓 系统镜像｜软件云盘|
    Disk|📁 手动备份|
    Disk|📁 文件归档|
    Disk|📺 视频照片｜编程教程|
    Disk|📺 视频音乐｜书籍漫画|System default shared folder
    IPC|IPC$|IPC Service ()
    Disk|home|Home directory of suowei.h
    SMB1 disabled -- no workgroup available
```

p.s. if you run into issue with the `smbclient` installed via `brew` on MacOS; You may try to resolve those via using the absolute path to the executable instead (use `/opt/homebrew/bin/smbclient`, instead of `smbclient`)





---

## Mount/Unmount Network Drive (MacOS)

The following section only apply to mounting/unmounting SMB volumes in MacOS system (if you are using Windows system, you can use `net use` command, if you are using Linux system you can use `cifs-utils`)

To mount network drive:

```
osascript -e 'mount volume "smb://$ip/$volume"'
osascript -e 'mount volume "smb://XXX.XXX.XXX.XXX/home"'
```

To unmount network drive:

```
diskutil unmount "/Volumes/${props.vol}"
diskutil unmount "/Volumes/home"
```

or

```
/usr/sbin/diskutil unmount "/Volumes/${props.vol}"
/usr/sbin/diskutil unmount "/Volumes/home"
```





