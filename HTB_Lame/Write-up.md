Start with a ping to check if server is up and answering to ICMP requests.
```bash
ping {target_ip}
```
Results:
![[ping.png]]

### Port enumeration
nmap scan:
```bash
nmap -p- -sC -sV {target_ip}
```
Results:
![[nmap_scan.png]]
5 ports were found to be open.

#### Checking if Anonymous access is allowed:
FTP:
anonymoys
![[ftp_anon.png]]
Nothing found

SMB:
![[smbclient.png]]
![[smbmap.png]]
![[smbclient_tmp.png]]
#### Searching for know exploits:
```bash
searchsploit vsftpd 2.3.4
```
results:
![[searchsploit_vsftpd.png]]
Failed to establish a shell.
![[exploit_vsftpd.png]]

![[searchsploit_samba.png]]
1 available in metasploit:
![[msf_search_samba.png]]
Successful becoming root.
![[root.png]]