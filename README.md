# 🔐 Evaluate Findings from Security Assessments

## 📌 Scenario
As a cybersecurity professional at **Structureality**, I performed a multi-layered security assessment to evaluate and strengthen the organization's security posture. This project covers:

- Dynamic Application Security Testing (DAST)
- Attack Surface Management (Email Security)
- Data Security Design (Classification)
- Web Application Firewall (ModSecurity)
- Vulnerability Scanning

This simulates a **real-world enterprise security workflow** aligned with **Zero Trust and defense-in-depth principles**.

---

## 🎯 Objectives
- Perform DAST using OWASP ZAP
- Identify and analyze vulnerabilities
- Reduce attack surface (email services)
- Implement data classification
- Configure and validate WAF (ModSecurity)
- Conduct vulnerability scans

---

## 🧪 Lab Environment

| System | Role |
|------|------|
| KALI VM | Security testing (ZAP, scanning) |
| LAMP VM | Web server (DVWA + ModSecurity) |
| MS10 | Mail / infrastructure services |
| DVWA | Vulnerable web application |

---

# 🕷️ Task 1: Dynamic Application Security Testing (DAST)

## 🔍 Objective
Use OWASP ZAP to simulate real-world attacks and identify vulnerabilities in a web application.

---

## ⚙️ Step 1: Launch OWASP ZAP
- Open OWASP ZAP from Kali
- Select **Automated Scan**

---

## 🌐 Step 2: Target Application

dvwa.structureality.com


---

## 🚀 Step 3: Run Scan
- Click **Attack**
- Wait until:

Attack complete


---

## 📸 ZAP Scan Execution
<p align="center">
  <img src="images/zap-scan.png" width="600">
</p>

---

## 📊 Step 4: Analyze Alerts

Focus on:
- 🔴 High Risk (Red)
- 🟠 Medium Risk (Orange)

---

## 📸 ZAP Alerts Dashboard
<p align="center">
  <img src="images/zap-alerts.png" width="600">
</p>

---

## 🚨 Key Findings

| Severity | Example Vulnerabilities | Impact |
|--------|----------------------|--------|
| 🔴 High | SQL Injection, Command Injection | Full compromise |
| 🟠 Medium | XSS, Missing Headers | Data exposure |
| 🟡 Low | Information Disclosure | Recon advantage |

---

## 🧠 Insight
DAST simulates attacker behavior and helps detect:
- Injection flaws
- Misconfigurations
- Input validation issues

---

# 🌐 Task 2: Network Reconfiguration

## 🎯 Objective
Move Kali into internal server subnet for deeper assessment.

---

## ⚙️ Step 1: Elevate Privileges
```bash
sudo su
⚙️ Step 2: Change Network (Lab UI)
Go to Resources tab
Set:
eth0 → vLAN_SERVERS
⚙️ Step 3: Refresh Network
nmcli conn down id 'Ethernet' && nmcli conn up id 'Ethernet'
⚙️ Step 4: Verify IP
ip a s eth0
📸 IP Verification
<p align="center"> <img src="images/ip-check.png" width="600"> </p>
✅ Expected Result
10.1.16.66
📧 Task 3: Attack Surface Management (Email)
🔍 Objective

Identify exposed email services and reduce attack surface.

⚙️ Scan Mail Server
nmap -sV 10.1.16.X
📸 Mail Server Scan
<p align="center"> <img src="images/mail-scan.png" width="600"> </p>
🚨 Findings
Open SMTP / IMAP / POP3 ports
Potential misconfigurations
Unsecured protocols
🔧 Remediation
Disable unused services
Enforce secure protocols (TLS)
Apply firewall rules
📂 Task 4: Data Security Design
🎯 Objective

Apply classification labels to sensitive data.

🏷️ Example Classification
Data Type	Label
Public Data	Public
Internal Docs	Internal
Sensitive Files	Confidential
📸 Data Classification
<p align="center"> <img src="images/data-classification.png" width="600"> </p>
🛡️ Task 5: Web Application Firewall (ModSecurity)
🎯 Objective

Deploy and validate ModSecurity to protect web applications.

⚙️ Enable ModSecurity
sudo nano /etc/modsecurity/modsecurity.conf

Set:

SecRuleEngine On
🔄 Restart Apache
sudo systemctl restart apache2
📸 ModSecurity Enabled
<p align="center"> <img src="images/modsecurity.png" width="600"> </p>
🧪 Test WAF
Run ZAP scan again
Confirm attacks are blocked
🔍 Task 6: Vulnerability Scanning
🎯 Objective

Identify system vulnerabilities and misconfigurations.

⚙️ Run Scan (OpenVAS / similar)
gvm-start
