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
- Target 1
  - CWE-552: Files or Directories Accessible to External Parties

<img src="https://github.com/edwardhough/wordpress-vuln/blob/main/images/image7.png" width=50% height=50%>
 
 - CWE-521: Weak Password Requirements
  - CWE-732: Incorrect Permission Assignment for Critical Resource
  - CWE-269: Improper Privilege Management




### Exploitation
_TODO: Fill out the details below. Include screenshots where possible._

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - `flag1.txt`: _TODO: Insert `flag1.txt` hash value_
    - **Exploit Used**
      - _TODO: Identify the exploit used_
      - _TODO: Include the command run_
  - `flag2.txt`: _TODO: Insert `flag2.txt` hash value_
    - **Exploit Used**
      - _TODO: Identify the exploit used_
      - _TODO: Include the command run_
