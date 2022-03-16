# Cybersecurity Red &amp; Blue Teaming Project

## Red Team: Summary of Operations
Table of Contents
Exposed Services
Critical Vulnerabilities
Exploitation
Exposed Services

**Nmap scan results for each machine reveal the below services and OS details:**
  __nmap -A 192.168.1.110 or nmap -sV 192.168.1.110__
  ![Nmap Scan Output](https://github.com/abge0386/Final-Project/blob/main/Screen%20Shots/Screen%20Shot%202022-03-14%20at%208.17.28%20PM.png)
  ![Nmap Scan Output 2](https://github.com/abge0386/Final-Project/blob/main/Screen%20Shots/Screen%20Shot%202022-03-14%20at%208.19.16%20PM.png)

This scan identifies the services below as potential points of entry:
Target 1
List of
Exposed Services
TODO: Fill out the list below. Include severity, and CVE numbers, if possible.
The following vulnerabilities were identified on each target:
Target 1
List of
Critical
Vulnerabilities
TODO: Include vulnerability scan results to prove the identified vulnerabilities.
Exploitation
TODO: Fill out the details below. Include screenshots where possible.
The Red Team was able to penetrate Target 1 and retrieve the following confidential data:
Target 1
flag1.txt: TODO: Insert flag1.txt hash value
Exploit Used
TODO: Identify the exploit used
TODO: Include the command run
flag2.txt: TODO: Insert flag2.txt hash value
Exploit Used
TODO: Identify the exploit used
TODO: Include the command run




# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology
The following machines were identified on the network:
- Name of VM 1
  - **Operating System**:
  - **Purpose**:
  - **IP Address**:
- Name of VM 2
  - **Operating System**:
  - **Purpose**:
  - **IP Address**:
- Etc.

### Description of Targets
_TODO: Answer the questions below._

The target of this attack was: `Target 1` (TODO: IP Address).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:
#### Name of Alert 1
_TODO: Replace `Alert 1` with the name of the alert._
Alert 1 is implemented as follows:
  - **Metric**: TODO
  - **Threshold**: TODO
  - **Vulnerability Mitigated**: TODO
  - **Reliability**: TODO: Does this alert generate lots of false positives/false negatives? Rate as low, medium, or high reliability.
#### Name of Alert 2
Alert 2 is implemented as follows:
  - **Metric**: TODO
  - **Threshold**: TODO
  - **Vulnerability Mitigated**: TODO
  - **Reliability**: TODO: Does this alert generate lots of false positives/false negatives? Rate as low, medium, or high reliability.
#### Name of Alert 3
Alert 3 is implemented as follows:
  - **Metric**: TODO
  - **Threshold**: TODO
  - **Vulnerability Mitigated**: TODO
  - **Reliability**: TODO: Does this alert generate lots of false positives/false negatives? Rate as low, medium, or high reliability.
_TODO Note: Explain at least 3 alerts. Add more if time allows._

### Suggestions for Going Further (Optional)
_TODO_: 
- Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain _how_ to implement each patch.
