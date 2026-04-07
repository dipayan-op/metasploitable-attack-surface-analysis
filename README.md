# metasploitable-attack-surface-analysis
# Metasploitable Attack Surface Analysis & Initial Access

This project simulates a real-world penetration testing scenario where a vulnerable system is analyzed to identify potential entry points and security weaknesses.

## Objective
To perform network scanning on a vulnerable machine (Metasploitable 2), identify exposed services, and analyze potential attack vectors.

---

## Lab Setup

- Attacker Machine: Kali Linux
- Target Machine: Metasploitable 2
- Network Type: NAT / Host-only

---

## Target IP

192.168.226.128

![Target IP](target-ip.png)
---

## Step 1: Network Scanning

### Command Used
nmap -sS -sV 192.168.226.128

### Scan Results

![Nmap Scan](nmap-scan-msf.png)

---

## Analysis of Open Ports

The target system exposes multiple services:

| Port | Service | Risk |
|------|--------|------|
| 21 | FTP (vsftpd 2.3.4) | Known backdoor vulnerability |
| 23 | Telnet | Unencrypted communication |
| 80 | HTTP (Apache) | Outdated version |
| 139/445 | SMB | High-risk attack surface |
| 3306 | MySQL | Database exposure |

---

## Risk Assessment

- FTP (vsftpd 2.3.4): 🔴 Critical
- Telnet: 🔴 High
- SMB: 🔴 High
- HTTP (Outdated Apache): 🟠 Medium

---

## Vulnerability Analysis

The FTP service is running vsftpd 2.3.4, which is known to contain a backdoor vulnerability (CVE-2011-2523).

This makes it a critical security risk, as attackers can potentially gain remote shell access.

Additionally, the presence of multiple open services such as Telnet, SMB, and MySQL significantly increases the attack surface.

---

## Step 2: FTP Access Test

### Command Used
ftp 192.168.226.128

### Result

![FTP Login](ftp-login.png)

---

## Analysis

- Anonymous login was successful
- No authentication required
- Directory access was allowed
- File upload was restricted (read-only access)

---

## Security Impact

This misconfiguration allows:
- Unauthorized access to the system
- Potential information disclosure
- Increased attack surface

---

## Exploitation: Telnet Access

### Command Used

telnet 192.168.226.128

### Credentials Used

Username: msfadmin  
Password: msfadmin  

---

## Successful Access

![Telnet login](telnet-login.png)

---

## Post-Exploitation Commands

After gaining access, the following commands were executed:

whoami  
id  
uname -a  
pwd  
ls  

---

## Analysis

The Telnet service allowed login using default credentials, which is a critical security misconfiguration.

This provided immediate shell access to the system without requiring advanced exploitation techniques.

---

## Security Impact

- Unauthorized access to system
- Full command execution capability
- Exposure of sensitive system information
- Increased risk of further exploitation

---

## Risk Assessment

- Telnet Service: 🔴 High Risk
- Weak Credentials: 🔴 Critical Risk

---

## Key Insight

Even simple misconfigurations like default credentials can lead to complete system compromise.

This highlights the importance of:
- Disabling insecure services
- Enforcing strong authentication
- Regular security auditing

---

## Skills Gained

- Network scanning using Nmap
- Service enumeration
- Identifying vulnerable services
- Basic penetration testing workflow
- Attack surface analysis

---
