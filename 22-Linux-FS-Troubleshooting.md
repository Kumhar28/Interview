## Detailed SSH troubleshooting steps for issues connecting to a Linux VM in Azure
### permission denyied
- Check autorised keys
- Check user name on server
-  `nmap -A 192.168.1.10` -- check which port is listning on remote server
- use -vvvv to verbose output
```bash
[root@foreman pulp]# nmap -A 192.168.1.35

Starting Nmap 6.40 ( http://nmap.org ) at 2024-03-21 06:54 EDT
Nmap scan report for 192.168.1.35
Host is up (0.0012s latency).
Not shown: 996 filtered ports
PORT     STATE  SERVICE   VERSION
22/tcp   open   ssh       OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 2048 ac:d8:0a:a8:6a:1f:78:6d:ac:06:8f:65:3e:ff:9c:8b (RSA)
|_256 e7:f8:b0:07:1c:5b:4a:48:10:bc:f6:36:42:62:6c:e0 (ECDSA)
80/tcp   closed http
443/tcp  closed https
9100/tcp closed jetdirect
MAC Address: 08:00:27:83:D3:06 (Cadmus Computer Systems)
Aggressive OS guesses: Linux 3.0 - 3.9 (93%), Linux 2.6.22 - 2.6.36 (91%), Linux 2.6.39 (90%), Linux 2.6.32 - 3.9 (89%), Linux 2.6.26 - 2.6.35 (89%), Crestron XPanel control system (88%), Netgear DG834G WAP or Western Digital WD TV media player (88%), HP P2000 G3 NAS device (88%), Ubiquiti AirMax NanoStation WAP (Linux 2.6.32) (88%), Linux 2.6.32 (88%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop

TRACEROUTE
HOP RTT     ADDRESS
1   1.21 ms 192.168.1.35

OS and Service detection performed. Please report any incorrect results at http://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 14.08 seconds
```
- telnet 192.168.1.10 22
- this will show connectivity
- check in `ssh_config` that `PasswordAuthentication yes`

### port 22 connenction refused
- ping the server
- check sshd service
- Wrong credentials and port
```bash
# chage juan
Changing the aging information for juan
Enter the new value, or press ENTER for the default
Minimum Password Age [0]: 10
Maximum Password Age [99999]: 90
Last Password Change (YYYY-MM-DD) [2006-08-18]:
Password Expiration Warning [7]:
Password Inactive [-1]:
Account Expiration Date (YYYY-MM-DD) [1969-12-31]:
```
- If port is open or close
- Check Firewall rules `firewall-save` if you see drop change it to Accept

### port 22 connenction timeout
- ping
- check firewall rules

### port 22 connenction failed
- check and delete key fingerprint from autorised keys

### ssh: Could not resolve hostname example.com: Name or service not known

### If user is locked then Check the lock status of any Linux Account
```bash
[root@jumphost ~]# usermod -L rajeev

[root@jumphost ~]# passwd -S rajeev
rajeev LK 2024-03-28 -1 -1 -1 -1 (Password locked.)

[root@jumphost ~]# usermod -U rajeev
[root@jumphost ~]# passwd -S rajeev
rajeev PS 2024-03-28 -1 -1 -1 -1 (Password set, SHA512 crypt.)
```

### Case 1: Password Locked
In this case the password of any account is locked using the below command
To lock the password
```bash
# passwd -l user1
Locking password for user user1.
passwd: Success
Review the status in /etc/shadow
```
```bash
# grep user1 /etc/shadow 
user1:!!$6$ciJaoDR9$Qpt9sctRLjbZ4/Agxy9UOvu/XQqNrFo9rpgfZ/xrF/8JphkEvF29ITpef0SVLdJcrpv8Q/.6mRAHee4tZT0r11:16299:0:99999:7:::
```
- As you can see above two exclamation mark `(!!)` before the encrypted password which means that the password has been locked

#### To unlock the password
```bash
# passwd -u user1
Unlocking password for user user1.
passwd: Success
```

### Case 2: Account is Locked
- In this case the user account might have been locked by the administrator
- To lock an account
```bash
# usermod -L user1
```
- Review your /etc/shadow file for the changes
```bash
# grep user1 /etc/shadow
user1:!$6$ciJaoDR9$Qpt9sctRLjbZ4/Agxy9UOvu/XQqNrFo9rpgfZ/xrF/8JphkEvF29ITpef0SVLdJcrpv8Q/.6mRAHee4tZT0r11:16299:0:99999:7:::
```
- As you see an extra single exclamation mark(!) appeared in the password section before the encrypted password starts which signifies that the user account is locked
- To unlock a user account
```bash
# usermod -U user1
```

### Case 3: Password never set
- This can also be the scenario where the administrator has not assigned any password due to which the user is not able to login
- So to verify this again you need to check your `/etc/shadow` file
```bash
# grep user1 /etc/shadow
user1:!!:16299:0:99999:7:::
```
- As you see two exclamation mark `(!!)` is there but no encrypted password which means a password is not set.
- If the password was set without lock your `/etc/shadow` would look like something below
```bash
# grep user1 /etc/shadow
user1:$6$ciJaoDR9$Qpt9sctRLjbZ4/Agxy9UOvu/XQqNrFo9rpgfZ/xrF/8JphkEvF29ITpef0SVLdJcrpv8Q/.6mRAHee4tZT0r11:16299:0:99
```

-------------------------------------------------------------------------------------------------------

## df is not showing all mounted filesystems
```bash
# df -Ph
Filesystem            Size  Used Avail Use% Mounted on
/dev/mapper/rootvg-rootvol  3.8G  1.7G  2.0G  45% /
/proc/mounts shows everything mounted fine.
```
### Resolution
- Rebooting will recreate the /etc/mtab file.
- If rebooting is not an option, as a temporary workaround, copying the contents of /proc/mounts to `/etc/mtab` will work:
```bash
# cat /proc/mounts > /etc/mtab
```
### Root Cause
- The server's `/etc/mtab` file was missing entries.
### Diagnostic Steps
- Since df pulls information from `/etc/mtab`, check to see if this file contains any data:
```bash
# cat /etc/mtab
/dev/mapper/rootvg-rootvol / ext3 rw 0 0
proc /proc proc rw 0 0
```
- In this case, only the root filesystem is listed in `/etc/mtab`, which is why only the root filesystem shows up with running `df`.

## Why df shows different device size then LVM command in Red Hat Enterprise Linux?
```bash
df -h

Raw
Filesystem                      Size  Used Avail Use% Mounted on
/dev/mapper/datavg-datalv        26G  1.1G   21G   5%   /data
lvs

Raw
  LV           VG               Attr            LSize   Pool 
 datalv    datavg             -wi-ao----       64.90G
```
### Resolution
- The filesystem should be recreated as the inode count is a way to high than the block count.
### Root Cause
- df displays the amount of disk space available on the file system.
- It does a calculation of blocks used and inodes used and determine the most accurate amount of space remaining on the filesystem.
- lvs, or any commands working at block device layer, will report the size of the block device. Basically, the quantity of space between the first block and the last block.
- df command will work at the file system level. In order to remain file system independent, it requests the number of blocks via statfs(2) system call, and use f_blocks as a base value for the size. As defined by statfs(2) man page, this is the "total data blocks in file system", which differs from the actual total number of blocks of the block device, and is file system specific.
- For example, in the case of an ext3 file system, among others, the data block reported will exclude from the total size the primary and backup superblocks, and will be calculated on the fly in each statfs(2) call.

```bash
Raw
                            count         blks each      blocks               size
diskblocks            17013760                 1           17013760      64.90   GiB(69.69 GB)
free                   6304446                 1           6304446       24.05   GiB(25.82 GB)
data blocks             252170                 1           252170        985.04  MiB(1.03  GB)
journal                      1                 32768       32768         128     MiB(134.22MB)
reserved                848122                 1           848122        3.24    GiB(3.47  GB)
metadata              10424376                 1           10424376      39.77   GiB(42.70 GB)
  superblocks               18                 1           18            72      KiB(73.73 KB)
  grp.descr.                18                 40          720           2.81    MiB(2.95  MB)
  reserved GDT              18                 991         17838         69.68   MiB(73.06 MB)
  data  bitmaps           5076                 1           5076          19.83   MiB(20.79 MB)
  inode bitmaps           5076                 1           5076          19.83   MiB(20.79 MB)
  inode tables            5076                 2048        10395648      39.66   GiB(42.58 GB)
    free             166318996                 0.0625      10394937.25   39.65   GiB(42.58 GB)
    in-use               11372                 0.0625      710.75        2.78    MiB(2.91  MB)
```
- 42Gb is occupied alone by the inode table.

## fsck check in detail

- The fsck command checks the integrity of a partition
- When running this command, you should do it with a non-active partition, this means = un-mounted, of course. 
- It also can perform interactive repairs on one or more Linux file systems.
- if the filesystem type is ext2, ext3, or ext4, then then you should use the e2fsck instead.
- Then run: `sudo fsck -p /dev/scb1` . The `-p` options tell fsck to automatically repair any problems that can be safely fixed without user intervention
- The difference between them is the approach, the fsck outputs a "clean" when is correct, the e2fsck performs and outputs a more complete and detailed scan.

```bash
[root@node01~]# e2fsck -f /dev/testvg/testlv
e2fsck 1.41.12 (17-May-2010)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
```

### Repair XFS FS
```bash
# dry run using -n
 xfs_repair -n /dev/sdb1

xfs_repair  /dev/sdb1
```

## XFS FS reduce

- At the moment, functionality to shrink XFS filesystems is not available in RHEL
- Use some backup/restore solution, such as xfsdump and xfsrestore. This may be useful especially if the filesystem is mostly empty.

Using the following procedure :

1) Backup the data using xfsdump
```bash
xfsdump -f /tmp/test.dump /test
```
2) Unmount the filesystem
```bash
umount /test
```
3) remove the filesystem and create new lv
```bash
lvremove /dev/vg00/lv00
lvcreate -L 400M /dev/vg00/lv00
```

4) Format the partition with xfs filesystem
```bash
mkfs.xfs -f /dev/vg00/lv00
```
5) Remount the filesystem
```bash
mount /dev/vg00/lv00 /test
```
6) Restore the data using xfsrestor
```bash
xfsrestore -f /tmp/test.dump /test
```

## Why does unmounting the filesystem returns error "device is busy" when lsof does not show any files held open in the memory?
- Oracle module was still using the filesystem /oracle

Diagnostic Steps
Checking for oracle modules still running
```bash
[root@server ~]# ps -ef|grep ora
root     13778 10765  0 12:14 pts/0    00:00:00 grep ora   <<<<<<  module exists
```
No files open in filesystem /oracle shown in lsof output and fuser output
```bash
[root@server ~]# lsof /oracle
[root@server ~]#

[root@server ~]# fuser -vm /oracle
[root@server ~]#
```
- Unmounting returns an error
```bash
[root@server ~]# umount /oracle
umount: /oracle: device is busy.
        (In some cases useful info about processes that use
         the device is found by lsof(8) or fuser(1))
```
- Checking the status of oracle module:
```bash
[root@server ~]# lsmod |grep ora
oracleacfs           3332147  0
oracleadvm            512629  0
oracleoks             510437  2 oracleacfs,oracleadvm
```
- Removing modules since the oracle application has already been shut down:
```bash
[root@server ~]# modprobe -vr oracleacfs
rmmod /lib/modules/2.6.32-431.1.2.el6.x86_64/weak-updates/usm/oracleacfs.ko

[root@server ~]# modprobe -vr oracleadvm
rmmod /lib/modules/2.6.32-431.1.2.el6.x86_64/weak-updates/usm/oracleadvm.ko
rmmod /lib/modules/2.6.32-431.1.2.el6.x86_64/weak-updates/usm/oracleoks.ko
```
- Checking the status of modules again and trying to unmount and this time unmount works
```bash
[root@server ~]# modprobe -vr oracleoks

[root@server ~]# lsmod | grep ora

[root@server ~]# umount /oracle
[root@server ~]#
```


## How to use the lsof command to troubleshoot Linux
- The `lsof` command, in combination with other tools like `top` or `ps`.
- It's commonly said that in Linux, everything is a file.

- For example, suppose you need to know what process is using a particular directory:
```bash
lsof /run
```
- Perhaps you need to know what files a particular process has open. This example looks at sshd:
```bash
lsof -p 22

COMMAND   PID USER   FD      TYPE DEVICE SIZE/OFF NODE NAME
kintegrit  22 root  cwd       DIR    8,2      224   64 /
kintegrit  22 root  rtd       DIR    8,2      224   64 /
kintegrit  22 root  txt   unknown                      /proc/22/exe

```
- COMMAND: The command name
- PID: Process ID (PID) of the process
- USER: Owner of the process
- FD: File descriptor definition
- TYPE: Type of file descriptor
- DEVICE: Device number or, in the case of a block device, character or other
- SIZE/OFF: Dimension of the file or offset (the suffix 0t is the offset)
- NODE: Node description of the local file; this could be the number of the local file, TCP, UDP, or STR (stream)
- NAME: The name of the mount point where the file resides

- You can also discover what files a particular user has open:
```bash
lsof -u admin
```

- For example, suppose you need to know what process uses a particular TCP port (like 22, for example):
```bash
lsof -i TCP:22
```
- You can also obtain a report on all network processes associated with a particular interface:
```bash
lsof -i TCP@127.0.0.1
```

## Security Weaknesses in Linux Software and Applications
- Keep software and applications up to date: Make sure to regularly apply updates and patches to fix known vulnerabilities.

### Configuration Errors
- Use strong passwords: Use strong, unique passwords for all accounts and avoid reusing passwords across multiple accounts.
- Restrict access to sensitive areas: Use access controls to restrict access to sensitive areas of the system to authorized users only.
- Disable unnecessary services: Only run services that are necessary for the system's operation, and disable any unnecessary services.

### Using the Security Features of Yum

https://www.liquidweb.com/kb/how-to-use-the-yum-history-command/

```bash
~]# yum check-update --security
Loaded plugins: langpacks, product-id, subscription-manager
rhel-7-workstation-rpms/x86_64                  | 3.4 kB  00:00:00
No packages needed for security; 0 packages available
```

### KVM
- When the qemu-kvm and libvirt packages are updated, it is necessary to stop all guest virtual machines, reload relevant virtualization modules (or reboot the host system), and restart the virtual machines.
```bash
~]# lsmod | grep kvm
kvm_intel             143031  0
kvm                   460181  1 kvm_intel
~]# modprobe -r kvm-intel
~]# modprobe -r kvm
~]# modprobe -a kvm kvm-intel
```

- Run `rpm -e PackageName` instead of `yum remove PackageName`. 
- The command `yum remove PackageName` removes the package binaries but can leave configuration files. 
- The command `rpm -e PackageName` removes everything related to a package, including the configuration files.

## The Importance of Patching and Patching Best Practices (Linux & Windows) 
- Understanding Patching  ( Security patch, Bug fixes, feature updates)
- Regular Assessment of Software 
- Prioritization of Patches 
- Testing Before Deployment 
- Scheduled Patching 
- Emergency Patching 
- 

## Finding largest top 10 files and directories On Linux / UNIX / BSD machine
```bash
sudo du -a /var/* | sort -n -r | head -n 10
sudo du -a /* | sort -n -r | head -n 10
```

## Is the file system is in read-only mode?

- You may end up getting an error such as follows when you try to create a file or save a file:
- Run mount command to find out if the file system is mounted in read-only mode:
```bash
mount
mount | grep '/ftpusers'
```

- To fix this problem, simply remount the file system in read-write mode on a Linux based system:
```bash
mount -o remount,rw /ftpusers/tmp
```

## Is my hard drive is dying?
```bash
smartctl -a /dev/DEVICE
# check for /dev/sda on a Linux server
smartctl -a /dev/sda
```

## XFS file-system doesn't get mounted, throws error metadata I/O error: block
- Check /var/log/messages
- mount: mount /dev/mapper/rhel-root on /mnt/sysimage failed: No space left on device
- lvextend -L +<size> VG/ThinPoolLV


## soft link and hardlink

### Hard Links 
 
- Each hard linked file is assigned the same Inode value as the original, therefore they reference the same physical file location. Hard links more flexible and remain linked even if the original or linked files are moved throughout the file system, although hard links are unable to cross different file systems.
- `ls -l` command shows all the links with the link column shows number of links.
- Links have actual file contents
- Removing any link, just reduces the link count, but doesn’t affect other links.
- Even if we change the filename of the original file then also the hard links properly work.
- We cannot create a hard link for a directory to avoid recursive loops.
- If original file is removed then the link will still show the content of the file.
- The size of any of the hard link file is same as the original file and if we change the content in any of the hard links then size of all hard link files are updated.
- The disadvantage of hard links is that it cannot be created for files on different file systems and it cannot be created for special files or directories.

### Soft Links 

- A soft link is similar to the file shortcut feature which is used in Windows Operating systems. Each soft linked file contains a separate Inode value that points to the original file. As similar to hard links, any changes to the data in either file is reflected in the other. Soft links can be linked across different file systems, although if the original file is deleted or moved, the soft linked file will not work correctly (called hanging link).
- `ls -l` command shows all links with first column value `l` and the link points to original file.
- Soft Link contains the path for original file and not the contents.
- Removing soft link doesn’t affect anything but removing original file, the link becomes “dangling” link which points to nonexistent file.
- A soft link can link to a directory.
- The size of the soft link is equal to the length of the path of the original file we gave. E.g if we link a file like ln -s /tmp/hello.txt /tmp/link.txt then the size of the file will be 14bytes which is equal to the length of the “/tmp/hello.txt”.
- If we change the name of the original file then all the soft links for that file become dangling i.e. they are worthless now.
- Link across file systems: If you want to link files across the file systems, you can only use symlinks/soft links.

## Azure VM Disk error

https://learn.microsoft.com/en-us/troubleshoot/azure/virtual-machines/linux-recovery-cannot-start-file-system-errors#repair-xfs-filesystem

- You can't connect to an Azure Linux virtual machine (VM) by using the Secure Shell Protocol (SSH), or the VM Agent status in the Azure portal isn't Ready. 
- When you run the `Boot diagnostics` in the Azure portal or connect to the `Serial Console`, you see log entries that resemble the following examples:

Boot into emergency mode
Fail to mount xfs filesystem
Fail to mount ext Logical Volume Manager (LVM) device

### Prevent boot failure
- If the nofail option is specified when mounting filesystems, the corruption of a non-critical filesystem may not prevent Linux from booting fully. 
- For more information about nofail, see Mount the disk. 
- Most mounts aside from the root (/), /usr, and /var can be done with nofail.

## How to set up LACP bonding interface on CentOS 7

Step 1: Load bonding kernel module
```bash
modprobe bonding
```
Step 2: Create bonding interface configuration file
- Create a new configuration file called ifcfg-bond0 in the directory /etc/sysconfig/network-scripts. We use our favorite text-editor nano to do so:
```bash
nano /etc/sysconfig/network-scripts/ifcfg-bond0
```
We will give this file the following content:
```bash
DEVICE=bond0
Type=Bond
NAME=bond0
BONDING_MASTER=yes
BOOTPROTO=none
ONBOOT=yes
IPADDR=89.207.131.xx
PREFIX=24
GATEWAY=89.207.131.1
NM_CONTROLLED=no
BONDING_OPTS="mode=4 miimon=100 lacp_rate=1"
```
- Please replace the IP address on the line IPADDR=89.207.131.xx with the main IP address of your server and GATEWAY=89.207.131.1 with the gateway which is correct for your IP address.

Step 3: Update physical interface configuration files
- It’s time to update the physical interface configuration files. Our server uses enp6s0 and enp7s0 as interfaces, so we start with enp6s0:
```bash
nano /etc/sysconfig/network-scripts/ifcfg-enp6s0
The content of this file is:

DEVICE=enp6s0
TYPE=Ethernet
BOOTPROTO=none
ONBOOT=yes
NM_CONTROLLED=no
IPV6INIT=no
MASTER=bond0
SLAVE=yes
```
We update enp7s0 next:
```bash
nano /etc/sysconfig/network-scripts/ifcfg-enp7s0
The content of this file is:

DEVICE=enp7s0
TYPE=Ethernet
BOOTPROTO=none
ONBOOT=yes
NM_CONTROLLED=no
IPV6INIT=no
MASTER=bond0
SLAVE=yes
```
Step 4: Reboot
Reboot your server with:
```bash
reboot
```
Step 5: Check bonding interface status
After reboot, your server should have bonding active. Check with:
```bash
cat /proc/net/bonding/bond0
```

### Types of modes

Runner :
- It is used to implement many kinds of NIC teaming using the JSON format concept. Various runners use team running modes as follows. 

- `Broadcast` –  Here data is sent over all interfaces.
- `Round-Robin` – Mode 0 Data is sent sequentially over all ports
- `Active-Backup` – One port or link is used at the same time while the other is kept as a backup
- `Lacp` –  This is 802.3ad Implements Link Aggregation Control Protocol
- `Loadbalance` – Active Tx – Load balancing and BPF-based Tx port selector. Traffic is sent over to all NICs.

- teamd nic teaming demon

- Teaming is a new feature,it handles the flows of packets more efficient than bonding does
```bash
modprobe team
```
```bash
BOOTPROTO=static
TEAM_CONFIG='{"runner":{"name":"activebackup"},"link_watch":{"name":"ethtool"}}'
IPADDR=192.168.122.120
NETMASK=255.255.255.0
GATEWAY=192.168.122.1
NAME=team0
DEVICE=team0
ONBOOT=yes
DEVICETYPE=Team
PREFIX=24
```
```bash
TEAM_MASTER=team0
TEAM_PORT_CONFIG='{"prio":99}'
DEVICETYPE=TeamPort
NAME=eth3
HWADDR=52:54:00:8c:33:ba
DEVICE=eth3
ONBOOT=yes
```

## Upgrade and Downgrade kernel
- Check current installed packages
```bash
rpm -qa | grep kernel
uname -r
```
### Downgrade Kernel
#### Method 1
```bash
# GRUB_DEFAULT=saved change value
# 0 :- current Kernel
# 1 :- Previous kernel
# 2 :- Previous to Previous kernel
[root@jumphost ~]# cat /etc/default/grub
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL_OUTPUT="console"
GRUB_CMDLINE_LINUX="crashkernel=auto spectre_v2=retpoline rhgb quiet"
GRUB_DISABLE_RECOVERY="true"
[root@jumphost ~]#
```
```bash
grub-mkconfig -o /boot/grub2/grub.cfg
```

#### Method 2
- saved_entry value change to 1 for previous
```bash
[root@jumphost ~]# cat /boot/grub2/grubenv
# GRUB Environment Block
saved_entry=CentOS Linux (3.10.0-1160.el7.x86_64) 7 (Core)
############################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################################[root@jumphost ~]#
```
```bash
grub-mkconfig -o /boot/grub2/grub.cfg
```

#### Method 3

- Run below command to set the kernel
-  This will change value in `/boot/grub2/grubenv`
```bash
grub2-set-default 1
```
- Make changes `grub.cfg` file

```bash
grub-mkconfig -o /boot/grub2/grub.cfg
```

### After patching, we boot with new kernel we are getting the error 
- Start VM
- Boot with by choosing rescue mode
```bash
grub2-set-default 1
```
- Make changes `grub.cfg` file

```bash
grub-mkconfig -o /boot/grub2/grub.cfg
```
- Reboot the VM


## Reinstall grub and how to recover
- `unknown filesyatem` error while system boot
- came `grub console`
```bash
grub> 
ls
```
- Exit from grub the boot the system with DVD media
- Run with `Troubleshooting` mode
- continue with 1 option

```bash
chroot /mnt/sysimage
# reinstall grub
grub2-install /dev/sda
# Regenerate the file
grub-mkconfig -o /boot/grub2/grub.cfg
```
- reboot the VM

## Build Initramfs
```bash
# dracut -f /boot/initramfs-<kernelVersion>.img <kernelVersion>
```
- IMPORTANT NOTE: Replace <kernelVersion> with the full version of the kernel you wish to rebuild.
- ﻿EXAMPLE: (for kernel version "4.18.0-305.19.1.el8_4.x86_64")
- Take backup first
```bash
# cp /boot/initramfs-4.18.0-305.19.1.el8_4.x86_64.img /boot/4.18.0-305.19.1.el8_4.x86_64.bak.$(date +%m-%d-%H%M%S).img

# dracut -f /boot/initramfs-4.18.0-305.19.1.el8_4.x86_64.img 4.18.0-305.19.1.el8_4.x86_64
```


## nfs client trobleshooting

https://nfs.sourceforge.net/nfs-howto/ar01s07.html

