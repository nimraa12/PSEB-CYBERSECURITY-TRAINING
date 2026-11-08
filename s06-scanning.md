


## Task A: Vulnerability Assessment-three complete findings

**Student Name:** Nimra Naveed

**Assessment Date:** 7th Nov.2026

---

## 1. Introduction

The purpose of this practical assignment is to perform network scanning, service enumeration, and vulnerability assessment on a deliberately vulnerable virtual machine named Metasploitable 2.

Kali Linux was used as the assessment machine, while Metasploitable 2 was used as the target system. Nmap was used to identify open ports, running services, and their versions. Additional checks were performed to investigate potential security weaknesses.

The assessment was conducted in an isolated virtual lab environment for educational purposes.

## 2. Objectives

The main objectives of this assignment are:

1. To identify the IP addresses of the attacker and target machines.
2. To verify network connectivity between Kali Linux and Metasploitable 2.
3. To perform network scanning using Nmap.
4. To identify open ports and running services.
5. To investigate potential vulnerabilities in the identified services.
6. To document three security findings with evidence and recommendations.
7. To understand how security weaknesses can affect a vulnerable system.

## 3. Lab Environment and Tools

| Component | Description |
|---|---|
| Attacker Machine | Kali Linux |
| Target Machine | Metasploitable 2 |
| Scanning Tool | Nmap |
| Network Analysis Tool | tcpdump |
| Connection Testing Tool | Netcat |
| Environment | Isolated Virtual Network |

## 4. Methodology

The assessment was performed using the following steps:

1. Started Kali Linux and Metasploitable 2 virtual machines.
2. Identified the IP addresses of both machines.
3. Verified connectivity using the ping command.
4. Performed an initial Nmap scan to identify open ports and services.
5. Investigated the identified services for potential security weaknesses.
6. Performed additional checks on selected ports.
7. Documented the findings, evidence, potential impact, and remediation recommendations.

## 5. Network Discovery and Scanning

### 5.1 Identifying the Kali Linux IP Address

The following command was executed in Kali Linux to identify its network configuration:

```bash
ip addr
```

The command displayed the available network interfaces and their assigned IP addresses.

<img width="808" height="275" alt="image" src="https://github.com/user-attachments/assets/5633efa0-54e8-4d45-9d74-e27f71680dc3" />


### 5.2 Identifying the Metasploitable 2 IP Address

The following command was executed on the Kali Linux machine:

```bash
sudo netdiscover -r 192.168.79.134
```

The command displayed the network interface configuration of the target machine.

<img width="671" height="232" alt="image" src="https://github.com/user-attachments/assets/8c16db06-b902-449d-8448-7e35afc0fb71" />


### 5.3 Testing Network Connectivity

To verify communication between the two virtual machines, the following command was executed from Kali Linux:

```bash
ping -c 4 192.168.79.131
```

<img width="528" height="217" alt="image" src="https://github.com/user-attachments/assets/8839067c-66b1-4d55-8372-d3454461b5ab" />


### 5.4 Initial Network Scan Using Nmap

An initial scan was performed to identify open ports and running services on the target machine.

Command:

```bash
sudo nmap -sC -sV -oA initial-nmap 192.168.199.131
```

**Explanation:**

- `sudo`: Runs Nmap with administrative privileges.
- `-sC`: Executes Nmap's default scripts.
- `-sV`: Attempts to identify service versions.
- `-oA`: Saves the scan results in multiple formats.
- The IP address specifies the target machine.

<img width="1029" height="763" alt="image" src="https://github.com/user-attachments/assets/98a5ce83-65b3-4abc-b3c9-3c970a42b583" />


# 6. Vulnerability Assessment Findings

Three security findings were selected from the services identified during the scan. Each finding is documented with its description, evidence, potential impact, and remediation recommendations.

## Finding 1: Potential Backdoor Associated with vsftpd 2.3.4

### 1. Title
Potential Backdoor Associated with vsftpd 2.3.4

### 2. Severity
**Reference Severity: Critical**

CVE-2011-2523 has a CVSS 3.1 score of 9.8 (Critical), with the following vector:

`CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`

**Important:** This score belongs to the CVE. The presence of vsftpd version 2.3.4 alone does not prove that the target contains the backdoor. The vulnerability's applicability must be verified.

### 3. Affected Asset

- Target IP: 192.168.79.131
- Service: FTP
- Port: 21
- Detected Version: vsftpd 2.3.4

### 4. Identifiers

- CVE: CVE-2011-2523
- CWE: Not assigned here
- CPE: Not independently verified

### 5. Description

The initial Nmap scan identified an FTP service running vsftpd version 2.3.4 on port 21.

This version is associated with CVE-2011-2523, which involved a malicious backdoor inserted into certain compromised downloads of the vsftpd 2.3.4 source code.

However, not every installation reporting version 2.3.4 is necessarily affected. The backdoor was associated with compromised downloads distributed between 30 June and 3 July 2011.

Therefore, additional verification is required before confirming that the target is vulnerable.

### 6. Evidence

The following command was used to identify the FTP service version:

```bash
nmap -sV -p 21 192.168.79.131
```

The following command was used to check for the known vsftpd backdoor:

```bash
sudo nmap -p 21 --script ftp-vsftpd-backdoor 192.168.79.131
```

<img width="835" height="226" alt="image" src="https://github.com/user-attachments/assets/80bb8eee-323c-4267-9efa-95fd75061cdd" />


<img width="947" height="425" alt="image" src="https://github.com/user-attachments/assets/1917d3a1-02f6-4450-bc26-c0443a7c63b1" />


### 7. Proof of Concept

The FTP service was identified using Nmap service detection. An additional Nmap script check was performed to investigate whether the known backdoor was present.

The version identification alone is not sufficient proof of successful remote code execution. No successful exploitation should be claimed unless independently demonstrated by actual test evidence.

### 8. Potential Impact

If the affected backdoor is present and exploitable, an attacker could potentially execute commands remotely without normal authentication.

Possible consequences include:

- Unauthorized access to the target system.
- Exposure of sensitive information.
- Modification or deletion of system files.
- Compromise of system confidentiality, integrity, and availability.

These impacts are conditional on the backdoor being present and successfully exploited.

### 9. Remediation

- Upgrade to a trusted and secure FTP service version.
- Obtain software only from official and verified sources.
- Verify software integrity before installation.
- Disable unnecessary FTP services.
- Restrict access to FTP using firewall rules.
- Monitor FTP connections and suspicious activities.

### 10. References

- https://nvd.nist.gov/vuln/detail/CVE-2011-2523
- https://www.cve.org/

---

## Finding 2: Use of Insecure Telnet Protocol

### 1. Title
Insecure Telnet Service Exposed on Port 23

### 2. Severity
**Severity: To Be Determined**

Telnet transmits communication without encryption. The final severity should be based on the system's exposure, the information transmitted, and the assessment evidence.

### 3. Affected Asset

- Target IP: 192.168.79.131
- Service: Telnet
- Port: 23
- Detected Service: Linux telnetd

### 4. Identifiers

- CWE-319: Cleartext Transmission of Sensitive Information
- CVE: Not identified for this finding
- CPE: Not independently verified

### 5. Description

The Nmap scan identified a Telnet service running on port 23 of the target machine.

Telnet is an older remote-access protocol that does not provide encryption for its communication. As a result, information transmitted through Telnet may be readable by someone who can capture the network traffic.

If credentials or other sensitive information are transmitted through this service, they may be exposed to unauthorized users.

### 6. Evidence

The following command was used to identify the Telnet service:

```bash
nmap -sV -p 23 192.168.79.131
```
<img width="798" height="238" alt="image" src="https://github.com/user-attachments/assets/ae5ad48b-a118-49db-95d9-f7bb0a9bb140" />

To investigate the communication, the following command can be used in a separate Kali Linux terminal:

```bash
sudo tcpdump -i any -nn -s0 -A 'host 192.168.79.131 and tcp port 23'
```
<img width="1640" height="180" alt="image" src="https://github.com/user-attachments/assets/0e72c3e4-fbdb-41ae-8535-91983af74fc7" />

A controlled connection can then be initiated from another terminal:

```bash
telnet 192.168.79.131
```
<img width="768" height="590" alt="image" src="https://github.com/user-attachments/assets/df0219d3-f90a-4485-b094-734053012d14" />


### 7. Proof of Concept

The Telnet service was identified through Nmap scanning. If packet capture was performed, the captured traffic can be examined to determine whether communication is transmitted in readable, unencrypted form.

The assessment should distinguish between identifying an exposed Telnet service and actually demonstrating sensitive information disclosure. Do not claim that credentials were captured unless the evidence clearly shows this.

### 8. Potential Impact

The use of unencrypted Telnet may result in:

- Exposure of login credentials.
- Disclosure of sensitive information.
- Unauthorized access if credentials are obtained.
- Increased risk of interception by an attacker with access to the network.

### 9. Remediation

- Disable Telnet if it is not required.
- Replace Telnet with SSH for secure remote administration.
- Restrict remote-access services using firewall rules.
- Avoid transmitting sensitive information over unencrypted connections.
- Monitor remote login attempts and network traffic.

### 10. References

- https://cwe.mitre.org/data/definitions/319.html
- https://www.rfc-editor.org/rfc/rfc854

---

## Finding 3: Exposed Bind Shell Service on Port 1524

### 1. Title
Exposed Bind Shell Service on Port 1524

### 2. Severity
**Severity: To Be Determined**

The risk may be critical if an unauthenticated remote shell is accessible and provides privileged access. The final severity must reflect the actual connection test and access level.

### 3. Affected Asset

- Target IP: 192.168.79.131
- Service: Bind Shell
- Port: 1524
- Environment: Metasploitable 2

### 4. Identifiers

- CVE: Not assigned for this specific finding
- CWE: No specific identifier assigned in this report
- CPE: Not independently verified

### 5. Description

During the initial network scan, port 1524 was identified as an open port on the Metasploitable 2 target machine.

This port is associated with a bind shell service in the Metasploitable 2 lab environment. A bind shell is a service that listens for incoming network connections and may provide command-line access to the system.

If the service allows remote access without appropriate authentication or authorization, it can create a serious security risk.

### 6. Evidence

The following command was used to investigate port 1524:

```bash
nmap -sV -p 1524 192.168.79.131
```

An additional connection check can be performed using Netcat:

```bash
nc -nv 192.168.79.131 1524
```

If a command prompt is provided, the following harmless commands can be used to identify the access level:

```bash
whoami
```

Exit the connection after the test:

```bash
exit
```

<img width="455" height="126" alt="image" src="https://github.com/user-attachments/assets/cdff1abd-8ebf-485c-a7a5-60f827e2df82" />


### 7. Proof of Concept

The Nmap scan identified port 1524 as open. Netcat can be used to test whether a connection to this port provides command-line access.

If the connection is successful, the output of the `whoami` commands can help identify the privileges of the connected session.

If the connection is unsuccessful, document the actual result and do not claim that remote shell access was obtained.

### 8. Potential Impact

If an unauthorized remote shell is accessible, an attacker may be able to:

- Execute commands on the target machine.
- Access files and system information.
- Modify system configurations.
- Obtain privileged access, depending on the permissions of the shell.
- Compromise the confidentiality, integrity, and availability of the system.

### 9. Remediation

- Disable unnecessary bind shell services.
- Remove unauthorized remote command services.
- Restrict access to port 1524 using firewall rules.
- Apply secure system configurations.
- Monitor open ports and unexpected listening services.
- Regularly conduct security assessments to identify exposed services.

### 10. References

- https://nmap.org/book/man-port-scanning-basics.html
- https://nmap.org/book/man.html

---

# 7. Summary of Findings

| No. | Finding | Port | Main Security Concern |
|---|---|---:|---|
| 1 | Potential vsftpd 2.3.4 backdoor | 21 | Possible remote code execution |
| 2 | Insecure Telnet service | 23 | Unencrypted communication |
| 3 | Exposed bind shell service | 1524 | Potential unauthorized remote shell access |

The findings represent three different security concerns: a potentially compromised FTP service, an insecure remote-access protocol, and an exposed remote shell service.

The verification status of each finding must be based on the actual commands and outputs collected during the assessment.

# 8. Conclusion

The vulnerability assessment was performed against the Metasploitable 2 virtual machine using Kali Linux and network scanning tools.

The initial Nmap scan identified multiple open ports and running services. Three services were selected for further investigation: vsftpd on port 21, Telnet on port 23, and a bind shell associated with port 1524.

The assessment demonstrated the importance of identifying exposed services, verifying their security configurations, and documenting potential weaknesses. It also highlighted that detecting a service version or an open port does not automatically confirm that a vulnerability has been successfully exploited.

Appropriate remediation measures, including disabling unnecessary services, using secure protocols, applying updates, and restricting network access, can help reduce the risk of unauthorized access.


# Task B: Assessment Activities

## B3 – Decoding CVSS Metrics for CVE-2011-2523

### 1. Introduction

The Common Vulnerability Scoring System (CVSS) is used to measure the severity of security vulnerabilities. It considers factors such as the method of attack, privileges required, user interaction, and the potential impact on a system.

The vulnerability CVE-2011-2523 is associated with a malicious backdoor in certain compromised downloads of vsftpd version 2.3.4.

**CVSS Version:** 3.1  
**Base Score:** 9.8  
**Severity:** Critical

### 2. CVSS Vector

```text
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```

### 3. Explanation of Each Metric

| Metric | Value | Plain-English Explanation |
|---|---|---|
| Attack Vector (AV) | Network (N) | The vulnerability can be exploited remotely through a network connection. An attacker does not need physical access to the target machine. |
| Attack Complexity (AC) | Low (L) | The attack does not require complicated conditions or special circumstances to succeed once the affected system is present. |
| Privileges Required (PR) | None (N) | The attacker does not need an existing account or authenticated access before attempting exploitation. |
| User Interaction (UI) | None (N) | No action from another user is required for the attack to succeed. |
| Scope (S) | Unchanged (U) | The impact remains within the security authority of the vulnerable component and does not cross into a separate security authority. |
| Confidentiality (C) | High (H) | Successful exploitation can allow an attacker to access sensitive information on the affected system. |
| Integrity (I) | High (H) | Successful exploitation can allow an attacker to modify or manipulate system data and resources. |
| Availability (A) | High (H) | Successful exploitation can affect the availability of the system and its resources. |

### 4. Overall Interpretation

The CVSS vector indicates that CVE-2011-2523 represents a serious security risk because it can be exploited remotely without requiring prior authentication or interaction from another user.

The high confidentiality, integrity, and availability impacts indicate that successful exploitation can compromise sensitive information, system data, and system availability.

The combination of these factors results in a CVSS score of 9.8, which falls into the Critical severity category.

### 5. Conclusion

Decoding the CVSS vector helps explain why CVE-2011-2523 is considered a critical vulnerability. The attack requires no prior privileges, can be initiated remotely, and may have serious consequences for the affected system.

Understanding individual CVSS metrics helps security professionals prioritize vulnerabilities and select appropriate remediation measures.

---

## B6 – Case Study: The vsftpd Supply-Chain Compromise

### 1. Introduction

In 2011, the vsftpd project experienced a supply-chain security incident involving version 2.3.4 of its FTP server software. Instead of exploiting a weakness in the original software, an attacker compromised the project's main download site and replaced the legitimate source-code archive with a modified version containing a malicious backdoor.

### 2. What Happened?

Between 30 June and 3 July 2011, a compromised version of the vsftpd 2.3.4 source-code archive was available through the project's main download server.

The modified source code contained a backdoor that could be triggered by a specially crafted FTP username containing the characters `:)`. When triggered, it attempted to open a command shell on TCP port 6200.

This could provide an attacker with unauthorized remote command execution on a system running the compromised build.

The important point is that the original vsftpd software was not inherently responsible for this incident. The problem was the malicious modification of the software distribution package.

### 3. How Was It Discovered?

The compromise came to the attention of the vsftpd project after a suspicious download archive was noticed and reported to the project's author, Chris Evans. The author investigated the modified source package and confirmed that it contained malicious code.

The incident was publicly reported in early July 2011. The compromised download was removed, and the project's official download location was moved.

The incident also highlighted the importance of verifying software signatures and checking the integrity of downloaded packages.

### 4. Modern Relevance

The vsftpd incident remains an important example of a software supply-chain attack. Modern organizations depend on external software libraries, open-source packages, third-party vendors, and automated software repositories.

If an attacker compromises any part of this distribution process, malicious code may reach organizations even when they believe they are downloading legitimate software.

The incident demonstrates the importance of:

- Downloading software from trusted and official sources.
- Verifying digital signatures and file hashes.
- Monitoring software dependencies.
- Securing source-code repositories and distribution servers.
- Maintaining a software inventory.
- Using software supply-chain security practices.

### 5. Conclusion

The vsftpd 2.3.4 incident demonstrated that software can become dangerous when its distribution process is compromised. It showed that organizations must verify not only the software they use but also the authenticity and integrity of the packages they download.

This incident remains relevant because modern cyberattacks frequently target software suppliers and distribution channels rather than directly attacking individual organizations.

### 6. References

1. The Register – Popular FTP package download tarball poisoned (2011):  
   https://www.theregister.com/security/2011/07/05/popular_ftp_package_download_tarball_poisoned/

2. NIST National Vulnerability Database – CVE-2011-2523:  
   https://nvd.nist.gov/vuln/detail/CVE-2011-2523

3. FIRST – Common Vulnerability Scoring System Version 3.1 Specification:  
   https://www.first.org/cvss/v3-1/specification-document

4. Nmap – vsftpd Backdoor Detection Script Documentation:  
   https://nmap.org/nsedoc/scripts/ftp-vsftpd-backdoor.html
