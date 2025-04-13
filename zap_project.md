# 🔐 Vulnerability Assessment – OWASP Juice Shop (ZAP + Nmap)

This project simulates a black-box vulnerability assessment of the **OWASP Juice Shop**, an intentionally vulnerable web app. The goal is to identify and report real-world security issues using open-source tools and the OWASP Top 10 framework.

---

## 🎯 Project Overview

- **Target App:** [https://juice-shop.herokuapp.com](https://juice-shop.herokuapp.com)
- **Test Type:** Black-box Web Application Scan
- **Tools Used:** OWASP ZAP, Nmap, SSL Labs, SecurityHeaders.com
- **Performed by:** Emmanuel Ilerioluwa Ajayi
- **Assessment Date:** April 7–8, 2025

---

## 🏗️ Environment Setup

### 1. Tool Installation

**OWASP ZAP:**

```bash
sudo apt install zaproxy
# or download manually from https://www.zaproxy.org/download/
```

**Nmap:**

```bash
sudo apt install nmap
```

Other tools:
- [SSL Labs](https://www.ssllabs.com/ssltest/)
- [SecurityHeaders.com](https://securityheaders.com/)

---

### 2. ZAP Proxy Configuration

To intercept and scan traffic:

- Set Firefox to use proxy: `127.0.0.1:8080`
- Open ZAP → Manual Explore or Spider
- Load Juice Shop in browser with ZAP listening

---

### 3. Nmap Recon

```bash
nmap -Pn juice-shop.herokuapp.com
```

- This showed multiple IPs and open ports (22, 80)

---

## 🔍 Vulnerability Discovery Workflow

### ZAP Steps:
1. **Spider the target** to map all pages
2. **Run Passive Scan** (automatic)
3. **Right-click → Active Scan** for dynamic analysis
4. View alerts sorted by risk (e.g. missing headers, input flaws)

### SSL & Header Analysis:
- Enter target URL in:
  - [SSL Labs](https://www.ssllabs.com/ssltest/)
  - [SecurityHeaders.com](https://securityheaders.com)

---

## 🔎 Findings Overview

| Vulnerability            | Severity     | Description                                              | OWASP Category              |
|--------------------------|--------------|----------------------------------------------------------|-----------------------------|
| Missing Security Headers | Medium       | Lacks CSP, HSTS, X-Content-Type-Options                  | A05: Security Misconfiguration |
| Secure SSL Configuration | Informational| SSL Labs grade A — no weak ciphers or protocol issues    | A02: Cryptographic Failures (Monitored) |
| Open Ports (22, 80)      | Low          | SSH and HTTP ports exposed via Nmap                     | A05: Security Misconfiguration |

---

## 🩹 Remediation Recommendations

```plaintext
1. Use Helmet.js in Node.js to apply HTTP headers securely.
2. Monitor TLS configuration regularly via SSL Labs.
3. Block port 22 to public or restrict to SSH key-auth only.
4. Redirect all HTTP traffic to HTTPS.
```

---

## 📁 Screenshots (in /screenshots)
<img width="1353" alt="Screenshot 2025-04-08 at 17 19 46" src="https://github.com/user-attachments/assets/7438e4ab-ce5d-4fab-9203-a7beb6585e99" />

<img width="1138" alt="Screenshot 2025-04-08 at 17 28 07" src="https://github.com/user-attachments/assets/a969367f-3619-41ca-850f-72ea19d5638a" />

<img width="847" alt="Screenshot 2025-04-08 at 17 00 53" src="https://github.com/user-attachments/assets/c934d296-14f6-4af0-8daf-ea9c7ca891a4" />

---

## 🔧 Tools Used

| Tool             | Role                            |
|------------------|----------------------------------|
| OWASP ZAP        | Scanning, spidering, fuzzing    |
| Nmap             | Port and service discovery      |
| SecurityHeaders  | Header policy verification      |
| SSL Labs         | TLS/SSL strength analysis       |


---

## ⚠️ Disclaimer

This test was performed on a publicly accessible, intentionally vulnerable environment (OWASP Juice Shop). No real-world systems or user data were affected. Always obtain written permission before conducting any security testing.
