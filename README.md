# Isolated-Cybersecurity-Home-Lab-Kali-ARM-DVWA-
Establish an ARM-native penetration testing environment using Kali Linux and the Damn Vulnerable Web Application (DVWA) in VirtualBox.
Goal:	Establish an ARM-native penetration testing environment using Kali Linux and the Damn Vulnerable Web Application (DVWA) in VirtualBox.	

System Specs	
Host OS: macOS (Apple Silicon M-series)

Attacker VM: Kali Linux (ARM64)

Target VM: DVWA (Running locally on Kali/ARM)

Hypervisor: Oracle VirtualBox

Key Hurdles & Solutions (The Value)	
1. ARM Architecture Incompatibility: Attempted to use Metasploitable 2/3 (x86), which failed on the ARM Mac. Solution: Switched to installing DVWA directly onto a compatible Kali ARM VM.

2. Virtual Disk Space: Ran out of space installing MariaDB. Solution: Used VBoxManage modifyhd on the host to resize the VDI, then GParted inside Kali to extend the partition.

3. DVWA Setup Failures: Encountered "Connection Timed Out" (DNS error) and "PHP Plain Text" (PHP handler failure). Solution: Manually fixed DNS (/etc/resolv.conf) and repeatedly used sudo a2enmod php8.3 to ensure the Apache handler was active.

Outcome: Successfully deployed a fully functional, isolated, and compatible hacking lab with DVWA accessible on http://127.0.0.1/dvwa/.
