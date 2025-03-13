# **Vulnerability Assessment & Remediation**

## **Project Overview**
This project involves conducting a **vulnerability assessment** using **OWASP ZAP** and **Nessus** on a Kali Linux virtual machine. The assessment focuses on identifying security weaknesses in web applications and network infrastructures, followed by remediation strategies to enhance security posture.

---

## **Tools & Technologies Used**
- **Operating System:** Kali Linux (running on VMware/VirtualBox)
- **Vulnerability Scanner:** OWASP ZAP, Nessus
- **Target System:** Intentionally vulnerable applications (e.g., DVWA, Metasploitable, WebGoat)
- **Reporting & Documentation:** Markdown, GitHub

---

## **1. Setting Up the Environment**

### **1.1 Installing Kali Linux on a Virtual Machine**
1. **Download and install VMware Workstation/VirtualBox**
   - [VMware Download](https://www.vmware.com/products/workstation-player.html)
   - [VirtualBox Download](https://www.virtualbox.org/)
2. **Download Kali Linux ISO**
   - [Kali Linux Official](https://www.kali.org/get-kali/)
3. **Create a New Virtual Machine:**
   - Allocate at least **4GB RAM, 2 CPU cores, and 30GB storage**
   - Install Kali Linux and update the system using:
     ```bash
     sudo apt update && sudo apt upgrade -y
     ```

**[Screenshot Placeholder]**: Kali Linux installation steps

### **1.2 Installing OWASP ZAP**
1. Open the terminal and install OWASP ZAP:
   ```bash
   sudo apt install zaproxy -y
   ```
2. Launch OWASP ZAP:
   ```bash
   zaproxy &
   ```
3. Configure your browser proxy to **localhost:8080** for traffic interception.

<img width="1073" alt="image" src="https://github.com/user-attachments/assets/7e1c7436-9963-45e1-b997-ebc2e98d0e4e" />


### **1.3 Installing Nessus**
1. Download Nessus for Linux from [Tenable](https://www.tenable.com/downloads/nessus)
2. Install Nessus:
   ```bash
   sudo dpkg -i Nessus*.deb
   ```
3. Start and enable the Nessus service:
   ```bash
   sudo systemctl start nessusd
   sudo systemctl enable nessusd
   ```
4. Access Nessus via browser: `https://localhost:8834`
5. Register for **Nessus Essentials** and activate with the provided key.

<img width="1439" alt="image" src="https://github.com/user-attachments/assets/a08effa4-84ad-4c20-b856-587fc8390941" />

---

## **2. Performing Vulnerability Assessments**

### **2.1 Scanning a Web Application with OWASP ZAP**
1. Open OWASP ZAP and enter the target URL (e.g., DVWA, WebGoat)
2. Start a **Passive Scan** by navigating through the application
3. Initiate an **Active Scan** to detect security flaws
4. Review the findings under the **Alerts tab**

<img width="1068" alt="image" src="https://github.com/user-attachments/assets/88c7ad31-0650-4bd1-88cc-b0cb1030e5fd" />


### **2.2 Network & System Scanning with Nessus**
1. Open Nessus and create a **New Scan**
2. Choose **Basic Network Scan** and enter the target IP (e.g., Metasploitable VM)
3. Run the scan and analyze detected vulnerabilities

**[Screenshot Placeholder]**: Nessus scan report

---

## **3. Remediation Strategies**
### **3.1 Interpreting OWASP ZAP Results**
- **Cross-Site Scripting (XSS):** Implement proper input validation
- **SQL Injection:** Use parameterized queries and ORM frameworks
- **Security Headers:** Enforce `X-Frame-Options`, `Content-Security-Policy`

### **3.2 Addressing Nessus-Detected Issues**
- **Patch outdated software** to fix vulnerabilities
- **Disable unnecessary services** to reduce attack surface
- **Restrict access using firewall rules**

---

## **4. Documentation & Reporting**
### **4.1 Generating OWASP ZAP Reports**
- Export scan results as **HTML, XML, or PDF**
- Document detected vulnerabilities and their fixes

### **4.2 Generating Nessus Reports**
- Export Nessus **vulnerability summary reports**
- Include recommended fixes in the final documentation

**[Screenshot Placeholder]**: OWASP ZAP & Nessus report samples

---

## **5. Lessons Learned & Next Steps**
- Regular vulnerability assessments help improve security posture
- Automating scans enhances efficiency
- Future plans: Expand testing to **cloud environments & CI/CD pipelines**
