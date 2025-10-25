# 🧠 Task 3 – OpenVAS Vulnerability Assessment

## 🎯 Objective
To perform an automated **vulnerability assessment** on a target system using **OpenVAS (Greenbone Vulnerability Management)** and analyze the discovered security issues, their impact, and mitigation strategies.

---

## 🧰 Tools & Environment
- **Tool:** OpenVAS / Greenbone Vulnerability Manager (GVM)
- **Operating System:** Kali Linux (VM)
- **Target:** Metasploitable Virtual Machine (`[REDACTED_IP]`)
- **Scan Type:** Full and Fast Scan
- **Date of Scan:** Oct 24, 2021

---

## ⚙️ Procedure

1. **Install and initialize OpenVAS**
   ```bash
   sudo apt install -y gvm
   sudo gvm-setup
   sudo gvm-start

Access OpenVAS Web UI at:
👉 [https://localhost:9392](https://localhost:9392)
(Login using the admin credentials created during setup.)

2. **Create a Target**

   * Target IP: `[REDACTED_IP]`
   * Port Range: Default (1–65535)
   * Alive Test: Consider alive

3. **Create and Run a Task**

   * Scan Config: *Full and Fast*
   * Target: `[REDACTED_IP]`
   * Task Name: *Metasploitable Scan*
   * Start Scan and wait for completion.

4. **Generate and Export Report**

   * Format: PDF / HTML / XML
   * Exported Report Name: `OpenVAS_Scan_[REDACTED_IP].pdf`

---

## 📊 Findings Summary

| Severity            | Count | Example Issues                                          |
| ------------------- | ----- | ------------------------------------------------------- |
| **High**            | 9     | Outdated OS, Weak Database Passwords, Command Execution |
| **Medium**          | 28    | SSL Expired, CSRF, SQL Injection                        |
| **Low**             | 2     | Minor misconfigurations                                 |
| **False Positives** | 0     | —                                                       |

**Key Vulnerabilities Identified:**

1. Outdated Ubuntu OS (EOL)
2. TWiki XSS & Command Execution
3. DistCC Remote Code Execution
4. Weak MySQL & PostgreSQL passwords
5. Apache Range Header DoS (CVE-2011-3192)
6. phpinfo() Information Disclosure
7. SSH Default Credentials
8. Tiki Wiki CMS Multiple Vulnerabilities
9. Expired SSL/TLS Certificates

---

## 🧩 Sample High-Severity Vulnerabilities

| Port     | Service      | Vulnerability                    | Severity | CVSS |
| -------- | ------------ | -------------------------------- | -------- | ---- |
| 80/tcp   | Apache httpd | Range Header DoS (CVE-2011-3192) | High     | 7.8  |
| 3306/tcp | MySQL        | Weak Root Password               | High     | 9.0  |
| 5432/tcp | PostgreSQL   | Weak Credentials                 | High     | 9.0  |
| 22/tcp   | SSH          | Default Credentials              | High     | 7.5  |
| 3632/tcp | DistCC       | Remote Code Execution            | High     | 9.3  |

---

## 🛡️ Mitigation Strategies

### 1. Outdated OS (EOL)

* Upgrade to a supported OS version (e.g., Ubuntu 22.04 LTS).
* Apply all security updates and patches regularly.
* Decommission legacy systems if not upgradable.

### 2. Weak / Default Credentials

* Enforce strong password policies for all accounts.
* Change default credentials immediately.
* Use SSH keys instead of password authentication.
* Restrict database logins to trusted hosts.

### 3. Web Application Vulnerabilities (TWiki, Tiki Wiki)

* Upgrade to patched versions.
* Implement input validation and output encoding.
* Deploy a Web Application Firewall (e.g., ModSecurity).
* Remove unnecessary plugins or outdated CMS modules.

### 4. DistCC Remote Code Execution

* Restrict access to trusted IP addresses only.
* Disable DistCC if not in use.
* Apply vendor patches.

### 5. Apache Range Header DoS

* Update Apache to version 2.2.20+ or 2.4.x.
* Enable `mod_reqtimeout` to limit request header sizes.
* Monitor web logs for abuse attempts.

### 6. phpinfo() File Disclosure

* Delete or restrict access to phpinfo files.
* Disable `display_errors` in `php.ini`.
* Use staging environments for configuration testing.

### 7. Expired SSL/TLS Certificates

* Renew SSL certificates and configure auto-renewal with Let’s Encrypt.
* Enforce TLS 1.2 or TLS 1.3 only.
* Disable weak ciphers and protocols.

---

## 🔍 Key Learnings

* Understood how OpenVAS identifies and categorizes vulnerabilities by severity.
* Learned to interpret CVSS scores and threat levels.
* Practiced mapping vulnerabilities to mitigation measures.
* Reinforced importance of continuous patching and secure configuration.

---

## 📁 Deliverables

* **Report:** `OpenVAS_Scan_[REDACTED_IP].pdf`
* **Findings Summary:** This README.md
* **Mitigation Report (optional):** `Task3_Mitigation_Strategies.pdf`
* **Screenshots:**

  * OpenVAS dashboard
  * Scan task results
  * Vulnerability details page

---

## 🏁 Conclusion

The OpenVAS vulnerability scan effectively identified multiple high-risk misconfigurations and outdated services on the target system.
Applying the above mitigation steps will significantly reduce the system’s attack surface and strengthen overall network security posture.
