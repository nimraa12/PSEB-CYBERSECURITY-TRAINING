Student Name: Nimra Naveed

Course: Digital Forensics and Cyber Security

Training: PSEB Cybersecurity Training

Assignment: Foundations – Day 1

Date: 24 October 2026

Task A – Malware Types
## Introduction

Malware (malicious software) is any software or code designed to damage computer systems, disrupt operations, steal information, or gain unauthorized access. Different types of malware use different methods to infect devices and achieve their objectives.

## 1. Malware Types and Real-World Examples

| Malware Type | Definition | Real-World Example and Year | Target | How It Spread | Primary Impact |
|---|---|---|---|---|---|
| **1. Virus** | A virus is malicious code that attaches itself to a legitimate file or program and replicates when the infected file is executed. | Brain Virus (1986) | IBM-compatible personal computers running MS-DOS. | Spread through infected floppy disks shared between computers. | Infected boot sectors and disrupted normal computer operations. |
| **2. Worm** | A worm is malware that can copy itself and spread between computers without needing to attach itself to another program. | Morris Worm (1988) | Computers connected to the early Internet, particularly UNIX systems. | Spread by exploiting weaknesses in network services and weak passwords. | Slowed down and disrupted thousands of computers and network services. |
| **3. Trojan** | A Trojan is malicious software disguised as a legitimate or useful application to trick users into installing it. | Zeus Trojan (2007) | Windows computers, particularly users of online banking services. | Spread through phishing emails, malicious downloads, and infected websites. | Stole banking credentials and financial information. |
| **4. Ransomware** | Ransomware is malware that blocks access to files or systems, usually by encrypting data, and demands payment to restore access. | WannaCry (2017) | Windows computers, including organizations, hospitals, and businesses worldwide. | Spread through vulnerable Windows systems by exploiting the EternalBlue vulnerability. | Encrypted files, disrupted services, and caused major financial losses. |
| **5. Spyware** | Spyware secretly monitors a user's activities and collects personal or confidential information without permission. | Pegasus (identified in 2016) | Smartphones belonging to targeted individuals, including journalists and activists. | Delivered through targeted malicious links and exploitation of vulnerabilities in mobile devices. | Collected private information and enabled unauthorized surveillance. |
| **6. Adware** | Adware is software that displays unwanted advertisements and may redirect users to suspicious websites. | Fireball (2017) | Windows and macOS computers using affected web browsers. | Spread through bundled software installations and other unwanted downloads. | Changed browser settings, displayed advertisements, and redirected web searches. |
| **7. Rootkit** | A rootkit is malicious software designed to hide its presence and other malicious activities while maintaining unauthorized access to a system. | ZeroAccess Rootkit (2011) | Windows-based computers. | Spread through malicious downloads and exploit-based infections. | Hid malicious processes, maintained access, and supported activities such as click fraud and cryptocurrency mining. |
| **8. Keylogger** | A keylogger records the keys typed by a user to capture sensitive information such as usernames and passwords. | HawkEye Keylogger (2013) | Windows computers used by individuals and organizations. | Commonly distributed through malicious email attachments and spam campaigns. | Captured keystrokes and stole login credentials and other sensitive information. |
| **9. Botnet Agent** | A botnet agent is malware that turns an infected device into a remotely controlled bot that can receive instructions from an attacker. | Mirai (2016) | Internet-connected devices, especially routers and IP cameras. | Spread by identifying devices with weak or default login credentials. | Created a large network of compromised devices used to launch distributed denial-of-service (DDoS) attacks. |
| **10. Fileless / Living-off-the-Land Malware** | Fileless malware uses system memory and legitimate operating-system tools to perform malicious activities while reducing the need to store traditional malware files on disk. | Astaroth (2018) | Windows computers, particularly business and personal systems. | Spread through phishing emails containing malicious links or shortcut files and abused legitimate Windows tools. | Stole sensitive information and credentials while making detection more difficult. |
| **11. Logic Bomb** | A logic bomb is malicious code that remains inactive until a particular condition, event, or date triggers it. | Michelangelo (1992) | Personal computers using affected disk storage and boot sectors. | Spread through infected floppy disks and other infected storage media. | Activated on a specific date and could overwrite important disk information, making data inaccessible. |
| **12. Bootkit** | A bootkit is malware that infects the boot process of a computer to load before the operating system and maintain hidden access. | TDL-4 (2011) | Windows-based computers. | Distributed through malicious downloads and exploit-based infections. | Modified the boot process, hid malicious components, and helped attackers maintain control of infected systems. |

## 2. Most Dangerous Malware Type for a Pakistani SME

Ransomware can be considered one of the most dangerous malware types for a small or medium-sized enterprise (SME) in Pakistan because it can encrypt important business files and interrupt daily operations. A business may lose access to customer records, financial documents, and essential systems, resulting in financial losses and damage to its reputation. SMEs with limited cybersecurity resources may face additional difficulties in recovering their data and restoring normal operations.

## B4 – File Encryption Using OpenSSL

### 1. Objective

The objective of this task is to encrypt a text file using OpenSSL, inspect the encrypted file header using the `xxd` command, and understand the purpose of the `Salted__` header.

### 2. Creating a Sample File

First, a separate directory was created for the practical exercise.

```bash
mkdir -p ~/B4-OpenSSL
cd ~/B4-OpenSSL
```

A sample text file was created using the following command:

```bash
echo "This is a sample file for the OpenSSL encryption practical." > sample.txt
```

The file contents were verified using:

```bash
cat sample.txt
```

<img width="721" height="304" alt="image" src="https://github.com/user-attachments/assets/628f31cf-0b04-42a8-8d59-e50a1241e6fc" />


### 3. Encrypting the File Using OpenSSL

The sample file was encrypted using AES-256-CBC encryption with OpenSSL.

```bash
openssl enc -aes-256-cbc -salt -pbkdf2 -iter 100000 -in sample.txt -out sample.txt.enc
```

A password was entered when prompted by OpenSSL.

**Explanation of the command:**

- `openssl enc`: Performs file encryption.
- `-aes-256-cbc`: Uses AES encryption with a 256-bit key in CBC mode.
- `-salt`: Adds a random salt during encryption.
- `-pbkdf2`: Uses PBKDF2 for password-based key derivation.
- `-iter 100000`: Specifies 100,000 key-derivation iterations.
- `-in sample.txt`: Specifies the original input file.
- `-out sample.txt.enc`: Specifies the encrypted output file.

### 4. Verifying the Encrypted File

The following command was used to check the files in the working directory:

```bash
ls -l
```

The first 32 bytes of the encrypted file were then examined using:

```bash
xxd -l 32 sample.txt.enc
```

**Explanation:**

The `xxd` command displays the hexadecimal representation of file contents. It helps inspect the encrypted file's header without attempting to read its encrypted contents as normal text.

<img width="768" height="315" alt="image" src="https://github.com/user-attachments/assets/1baf8975-b29d-414a-a39b-f97692b5382e" />


### 5. Understanding the Salted__ Header

The encrypted file begins with a header containing the text `Salted__` when OpenSSL uses its traditional salted file format.

Its hexadecimal representation is:

```text
53 61 6c 74 65 64 5f 5f
```

**Explanation:**

The `Salted__` header indicates that a salt value is stored in the encrypted file. A salt is random data used during password-based key derivation. It helps ensure that encrypting different files with the same password does not automatically produce the same derived encryption key.

### 6. Decrypting the File

To verify that the encryption process was successful, the encrypted file was decrypted using the following command:

```bash
openssl enc -d -aes-256-cbc -pbkdf2 -iter 100000 -in sample.txt.enc -out decrypted.txt
```

The same password used during encryption was entered when prompted.

The original and decrypted files were compared using:

```bash
diff -s sample.txt decrypted.txt
```

<img width="773" height="181" alt="image" src="https://github.com/user-attachments/assets/b24d5a14-2d01-4d0b-ae16-e7145d9b1242" />

This confirms that the encrypted file was successfully decrypted and its contents matched the original file.

### 7. Result

The practical demonstrated how OpenSSL can encrypt a text file using AES-256-CBC and password-based key derivation. The encrypted file was inspected using `xxd`, and the `Salted__` header was identified. Finally, the file was decrypted successfully and compared with the original file.

## B5 – Man-in-the-Middle (MITM) Attack Case Study

### Case Study: Lenovo Superfish Incident (2015)

**1. Introduction**

A Man-in-the-Middle (MITM) attack occurs when an unauthorized party intercepts communication between two parties without their knowledge. The attacker may monitor or modify the information being exchanged.

**2. Who Was Involved?**

In 2015, Lenovo faced a security issue involving Superfish VisualDiscovery, an advertising application pre-installed on some consumer laptops. The software created a security weakness by intercepting encrypted web traffic.

**3. How Did the Incident Happen?**

Superfish installed a self-signed root Certificate Authority (CA) certificate into the computer's trusted certificate store. This allowed the software to intercept HTTPS connections, decrypt the traffic, and then re-encrypt it before sending it to the browser.

The major problem was that the certificate's private key was not adequately protected and could be recovered. This created an opportunity for an external attacker to imitate trusted websites and intercept encrypted communications without triggering normal browser certificate warnings.

**4. What Information Was at Risk?**

The weakness could expose sensitive information transmitted through affected web browsers, including:

- Login usernames and passwords.
- Personal information.
- Email communications.
- Banking and other confidential website information.

This was a serious privacy and security risk. However, the existence of this vulnerability does not by itself prove that external attackers successfully stole users' information.

**5. What Security Controls Could Have Prevented It?**

The incident could have been prevented or reduced through:

- Avoiding the installation of unnecessary and untrusted root certificates.
- Protecting private cryptographic keys and never reusing them across devices.
- Properly validating HTTPS certificates.
- Performing security testing before distributing pre-installed software.
- Monitoring unexpected changes to trusted certificate stores.
- Promptly removing vulnerable applications and certificates.

**6. Cost and Impact**

The incident damaged customer trust in Lenovo and raised concerns about user privacy and the security of pre-installed software. Lenovo had to address the issue, disable the software's server-side activity, and provide removal instructions. The vulnerability also created potential financial, legal, and reputational consequences.

**7. Conclusion**

The Lenovo Superfish incident demonstrates how incorrectly implemented certificate-based security can weaken HTTPS protection. It highlights the importance of secure certificate management, software testing, and protecting users' confidential information.

### References

1. US-CERT – Lenovo Superfish Adware Vulnerable to HTTPS Spoofing: https://seclists.org/cert/2015/103
2. Lenovo – Superfish Security Advisory: https://support.lenovo.com/lt/en/product_security/superfish
3. CERT/CC – Vulnerability Note VU#529496: https://www.kb.cert.org/vuls/id/529496/
4. Lenovo – Official Statement on Superfish: https://news.lenovo.com/pressroom/press-releases/lenovo-statement-on-superfish/
