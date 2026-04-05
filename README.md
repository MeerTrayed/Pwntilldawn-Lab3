# Pwntilldawn-Lab3
1. Looking for ip
   `nmap -sn 10.150.150.0/24` (or even better do this)
   `nmap -p 80,21,22,445 10.150.150.0/24`

Note this for:
  This tells Nmap to ONLY scan specific ports instead of all ports: <br/>
80 → HTTP (web server)
21 → FTP (file transfer)
22 → SSH (remote login)
445 → SMB (Windows file sharing)
(Picture here)

Doing 10.150.150.11 <br/>
Has 
| Service  |  State 
| ------------- | ------------- |
| ftp | Close  | 
| ssh  | Close  |
| http  | Close  |
| microsoft-ds  | Close  | <br/>

 2.`gobuster dir -u http://10.150.150.11 -w /usr/share/wordlists/dirb/common.txt -x php,txt,bak`
 
