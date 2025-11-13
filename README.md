# Isolated-Cybersecurity-Home-Lab-Kali-ARM-DVWA-
# ⚙️ ISOLATED CYBERSECURITY HOME LAB: KALI (ARM64) + DVWA

This document details the setup and troubleshooting required to build a functional, isolated Penetration Testing lab environment on an Apple Silicon (ARM64) host.

## 🖥️ System & Environment
* **Host OS:** macOS (Apple Silicon M-series)
* **Attacker VM:** Kali Linux (ARM64)
* **Target:** DVWA (Damn Vulnerable Web Application) running locally on Kali.
* **Hypervisor:** Oracle VM VirtualBox

---

## 💥 Key Hurdles Encountered & Solutions

| Hurdle | Cause | Solution |
| :--- | :--- | :--- |
| **1. Architecture Conflict** | Metasploitable 2/3 and public Docker images were all x86, incompatible with ARM64. | Abandoned incompatible images. Switched to manually installing LAMP/DVWA directly onto the Kali ARM VM. |
| **2. Insufficient Disk Space** | Default 18GB disk ran out of space during MariaDB installation. | **1.** Shut down Kali. **2.** Ran `VBoxManage modifyhd` on the Mac host to resize the VDI to 50GB. **3.** Used `sudo gparted` inside Kali to expand the partition. |
| **3. Networking (Git Clone Fails)** | Kali was unable to resolve DNS names to connect to GitHub (`Connection timed out`). | Manually fixed DNS by editing `/etc/resolv.conf` to use `nameserver 8.8.8.8` (Google DNS). |
| **4. Web Server Not Processing PHP** | Apache was serving the DVWA config file as plain text (PHP execution was disabled). | **1.** Confirmed MariaDB/Apache installation using correct packages. **2.** Fixed the `DocumentRoot` in `/etc/apache2/sites-available/000-default.conf`. **3.** Ensured the PHP handler was active. |
| **5. Database Connection Failed** | MariaDB root user's authentication method was incompatible with PHP. | Logged into MariaDB console and ran `SET PASSWORD FOR 'root'@'localhost' = PASSWORD('');` to enable legacy login compatibility. |

---

## ✅ Final Outcome
The lab is fully functional. DVWA is accessible at **http://127.0.0.1/dvwa/** and ready for penetration testing projects.
