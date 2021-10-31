
# My File Server-1 Walkthrough
https://www.vulnhub.com/entry/my-file-server-1,432/




## Roadmap

Penetrating Methodologies

- Network Scanning (Nmap, netdiscover)

- Add more integrations


## Network Scanning

Using Nmap 
```bash
  nmap -sn 192.168.56.24/24
```
```bash
┌──(root💀kali)-[~]
└─# nmap -sn 192.168.56.1/24  
Starting Nmap 7.91 ( https://nmap.org ) at 2021-10-31 11:10 IST
Nmap scan report for 192.168.56.129
Host is up (0.00091s latency).
MAC Address: 00:0C:29:4E:44:EE (VMware)
Nmap scan report for 192.168.56.254
Host is up (0.00055s latency).
MAC Address: 00:50:56:E3:F3:D7 (VMware)
Nmap scan report for 192.168.56.128
Host is up.
Nmap done: 256 IP addresses (3 hosts up) scanned in 6.33 seconds

```
Using Netdiscover
```bash
  netdiscover -i eth1 -r 192.168.56.0/24
```
```bash
 Currently scanning: Finished!   |   Screen View: Unique Hosts                                                      
                                                                                                                    
 11 Captured ARP Req/Rep packets, from 2 hosts.   Total size: 660                                                   
 _____________________________________________________________________________
   IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 192.168.56.129  00:0c:29:4e:44:ee      4     240  VMware, Inc.                                                     
 192.168.56.254  00:50:56:e3:f3:d7      7     420  VMware, Inc.                                                     
```
Nmap Port Scanning
```bash
  
┌──(root💀kali)-[~]
└─# nmap -sC -sV 192.168.56.129
Starting Nmap 7.91 ( https://nmap.org ) at 2021-10-31 07:17 IST
Stats: 0:00:14 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 100.00% done; ETC: 07:17 (0:00:00 remaining)
Nmap scan report for 192.168.56.129
Host is up (0.0013s latency).
Not shown: 908 filtered ports, 85 closed ports
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 3.0.2
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_drwxrwxrwx    3 0        0              16 Feb 19  2020 pub [NSE: writeable]
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:192.168.56.128
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 2
|      vsFTPd 3.0.2 - secure, fast, stable
|_End of status
22/tcp   open  ssh         OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 
|   2048 75:fa:37:d1:62:4a:15:87:7e:21:83:b9:2f:ff:04:93 (RSA)
|   256 b8:db:2c:ca:e2:70:c3:eb:9a:a8:cc:0e:a2:1c:68:6b (ECDSA)
|_  256 66:a3:1b:55:ca:c2:51:84:41:21:7f:77:40:45:d4:9f (ED25519)
80/tcp   open  http        Apache httpd 2.4.6 ((CentOS))
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/2.4.6 (CentOS)
|_http-title: My File Server
111/tcp  open  rpcbind     2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100003  3,4         2049/udp   nfs
|   100003  3,4         2049/udp6  nfs
|   100005  1,2,3      20048/tcp   mountd
|   100005  1,2,3      20048/tcp6  mountd
|   100005  1,2,3      20048/udp   mountd
|   100005  1,2,3      20048/udp6  mountd
|   100021  1,3,4      37448/udp   nlockmgr
|   100021  1,3,4      37665/udp6  nlockmgr
|   100021  1,3,4      42929/tcp   nlockmgr
|   100021  1,3,4      50321/tcp6  nlockmgr
|   100024  1          38678/udp   status
|   100024  1          39215/tcp   status
|   100024  1          40578/tcp6  status
|   100024  1          55636/udp6  status
|   100227  3           2049/tcp   nfs_acl
|   100227  3           2049/tcp6  nfs_acl
|   100227  3           2049/udp   nfs_acl
|_  100227  3           2049/udp6  nfs_acl
445/tcp  open  netbios-ssn Samba smbd 4.9.1 (workgroup: SAMBA)
2049/tcp open  nfs_acl     3 (RPC #100227)
2121/tcp open  ftp         ProFTPD 1.3.5
MAC Address: 00:0C:29:4E:44:EE (VMware)
Service Info: Host: FILESERVER; OS: Unix

Host script results:
|_clock-skew: mean: 3h39m59s, deviation: 3h10m31s, median: 5h29m58s
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.9.1)
|   Computer name: localhost
|   NetBIOS computer name: FILESERVER\x00
|   Domain name: \x00
|   FQDN: localhost
|_  System time: 2021-10-31T12:47:46+05:30
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-10-31T07:17:49
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 53.72 seconds
```
