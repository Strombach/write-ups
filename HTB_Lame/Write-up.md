Start with a ping to check if server is up and answering to ICMP requests.
```bash
ping {target_ip}
```
Results:
![[img/ping.png]]

### Port enumeration
nmap scan:
```bash
nmap -p- -sC -sV {target_ip}
```
Results:
![[img/nmap_scan.png]]
5 ports were found to be open.

#### Checking if Anonymous access is allowed:
FTP:
anonymoys
![[img/ftp_anon.png]]
Nothing found

SMB:
![[smbclient.png]]
![[img/smbmap.png]]
![[img/smbclient_tmp.png]]
#### Searching for know exploits:
```bash
searchsploit vsftpd 2.3.4
```
results:
![[img/searchsploit_vsftpd.png]]
Failed to establish a shell.
![[exploit_vsftpd.png]]

![[img/searchsploit_samba.png]]
1 available in metasploit:
![[img/msf_search_samba.png]]
Successful becoming root.
![[img/root.png]]