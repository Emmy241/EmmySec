# 🔐 DVWA + Nessus Vulnerability Assessment (OWASP-Aligned)

This project simulates a real-world web application security assessment using **DVWA** (Damn Vulnerable Web Application) and **Tenable Nessus Essentials**. The goal was to identify vulnerabilities, match them to the **OWASP Top 10**, and provide remediation strategies in a clean, client-style report.

---

## 🧠 Project Objectives

- Set up a vulnerable web app (DVWA) on a local server
- Perform a comprehensive Nessus scan (Advanced Policy)
- Identify real-world CVEs affecting OpenSSL, PHP, and web configs
- Map findings to **OWASP Top 10** risks
- Document findings with actionable fixes and reporting

---

## 🛠 Tools & Technologies Used

| Tool              | Purpose                                     |
|-------------------|---------------------------------------------|
| DVWA              | Target vulnerable app                       |
| XAMPP             | Apache + MySQL stack for DVWA               |
| Nessus Essentials | Automated vulnerability scanning            |
| OWASP Top 10      | Threat modeling and mapping                 |
| Kali Linux        | Recon and enumeration tools      |

---

## 🏗️ Environment Setup

### DVWA + XAMPP Setup

```bash
# Clone DVWA
git clone https://github.com/digininja/DVWA.git

# Move DVWA to web directory (XAMPP or Apache2)
mv DVWA /opt/lampp/htdocs/

# Start XAMPP
sudo /opt/lampp/lampp start
```

- Visit `http://127.0.0.1/dvwa/setup.php` to initialize the database
- Login: `admin` / `password`
- Set security level to `Low` in the DVWA settings page

---

## 📡 Nessus Scan Execution

### Scan Configuration

- **Scan Type**: Advanced Scan
- **Target**: `127.0.0.1` or local network IP
- **Plugins Enabled**: Web Servers, General, Apache, CGI, PHP
- **Port Range**: default

After launching the scan, I reviewed all vulnerabilities flagged in the report and correlated them to OWASP risks.

---

## 🔎 Key Vulnerabilities Identified

| Vulnerability                  | Severity   | OWASP Category              | Description                                      |
|-------------------------------|------------|-----------------------------|--------------------------------------------------|
| OpenSSL < 1.1.1za             | Critical   | A02: Cryptographic Failures | Vulnerable crypto library                        |
| PHP < 8.3.19                  | High       | A06: Vulnerable Components  | Known RCE & security issues                      |
| HTTP TRACE Method Enabled     | Medium     | A05: Security Misconfiguration | Allows XST attack vectors                     |
| Multiple OpenSSL CVEs         | Medium     | A02: Cryptographic Failures | Weak cipher negotiation                          |

---

<img width="1238" alt="Screenshot 2025-04-13 at 12 54 54" src="https://github.com/user-attachments/assets/ea07c04a-ff3a-4ca1-82f6-afb7f1cfdc09" />
<img width="1232" alt="Screenshot 2025-04-13 at 12 46 14" src="https://github.com/user-attachments/assets/90e5832d-5a96-42dd-8d0d-e9f598c3db35" />
<img width="1214" alt="Screenshot 2025-04-13 at 12 41 19" src="https://github.com/user-attachments/assets/f780554c-b15e-4f5e-9415-28c10c4830ff" />
<img width="1238" alt="Screenshot 2025-04-13 at 12 39 51" src="https://github.com/user-attachments/assets/73ad4c2e-e17c-45d2-a022-1435b309cdf1" />
<img width="1211" alt="Screenshot 2025-04-13 at 12 38 36" src="https://github.com/user-attachments/assets/28ed3202-4af7-425d-bb8e-a55422fcb501" />

---

## 🩹 Remediation Steps

### 1. Upgrade OpenSSL

```bash
sudo apt update
sudo apt install openssl
openssl version  # Ensure it's 1.1.1za or later
```

### 2. Update PHP

```bash
sudo apt install php8.3
php -v
```

### 3. Disable HTTP TRACE

#### Apache:
```apache
TraceEnable off
```

#### Nginx:
```nginx
if ($request_method ~* TRACE) {
    return 405;
}
```

---

## 🔍 OWASP Top 10 Mapping (Covered)

| OWASP Category                  | Identified in Scan |
|--------------------------------|--------------------|
| A02: Cryptographic Failures     | ✅                 |
| A05: Security Misconfiguration  | ✅                 |
| A06: Vulnerable Components      | ✅                 |

*Other categories will be covered in future test phases.*

---

## 📁 Project Structure


dvwa-nessus-vuln-assessment/
├── README.md
├── Nessus_Vuln_Report_DVWA.pdf
├── scan_output.nessus (optional)
└── screenshots/
    ├── nessus_dashboard.png
    ├── openssl_cve.png
    ├── php_version.png
    └── http_trace.png

---

## ⚖️ Legal & Ethical Note

This project was conducted in a safe and legal test environment using DVWA. No real systems or sensitive data were harmed. Always obtain written permission before testing external systems.

---
