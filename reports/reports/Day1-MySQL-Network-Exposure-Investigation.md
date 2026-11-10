# Day 1 – MySQL Network Exposure Investigation

## 1. Objective
Identify exposed network services on a Windows host, investigate MySQL connectivity, evaluate firewall configurations, and apply remediation.

## 2. Lab Environment
- Host OS: Windows
- Security testing OS: Kali Linux
- Virtualization: VMware Workstation
- Network mode: NAT
- Scanning tool: Nmap 7.99

## 3. Initial Discovery

Target addresses:
- Windows VMware adapter: 192.168.189.1
- Windows Wi-Fi adapter: 192.168.1.11
- Kali Linux: 192.168.189.128

Nmap identified:
- TCP 3306 – MySQL
- TCP 33060 – MySQL X Protocol

Both ports were reachable from Kali Linux.

## 4. Investigation

Identified MySQL Server 8.0 running as Windows service MySQL80.

Configuration file:
`C:\ProgramData\MySQL\MySQL Server 8.0\my.ini`

Windows Firewall investigation identified two enabled inbound Allow rules:
- Port 3306
- Port 33060

Both rules had LocalAddress = Any and RemoteAddress = Any.

## 5. Security Finding

MySQL services were reachable from the Kali Linux virtual machine through both the VMware and Wi-Fi target addresses.

This represented a potential network exposure because inbound access was not restricted by the identified firewall rules.

## 6. Remediation

Disabled the unnecessary inbound firewall exceptions for TCP ports 3306 and 33060.

## 7. Validation

Repeated Nmap TCP connection scans after remediation.

Result:
- TCP 3306: Filtered
- TCP 33060: Filtered

The results indicate that the firewall is now blocking or filtering the tested connection attempts.

## 8. Conclusion

The investigation demonstrated network reconnaissance, service identification, Windows process investigation, firewall analysis, security remediation, and post-remediation validation.

The unnecessary inbound firewall exceptions were disabled, reducing MySQL network exposure from the tested Kali Linux environment.

## 9. Tools Used
- Kali Linux
- Nmap
- Windows PowerShell
- Windows Defender Firewall
- VMware Workstation
- Git and GitHub