# SIEM Log Monitoring with Splunk

## 📌 Introduction

Security Information and Event Management (SIEM) solutions are essential for detecting, analyzing, and responding to cybersecurity threats. This project demonstrates how to set up **Splunk** on Kali Linux, ingest system logs, configure a **Splunk Forwarder**, and create alerts for security insights.

## 🎯 Objectives

- Deploy **Splunk** on **Kali Linux** for log analysis.
- Ingest system logs and monitor security events.
- Configure **Splunk Forwarder** for remote log collection.
- Create queries and visualizations to detect anomalies.
- Set up **alerts** for suspicious activity detection.
- Enhance log management for **threat detection and incident response**.

---

## 🛠️ Setup & Installation

### **Step 1: Download & Install Splunk**

1. **Download Splunk** (Free Version for Personal Use) from the official site: [Splunk Downloads](https://www.splunk.com/en_us/download.html)
2. Install using the `.deb` package:
   ```bash
   sudo dpkg -i splunk*.deb
   ```
3. Enable Splunk service:
   ```bash
   sudo /opt/splunk/bin/splunk enable boot-start
   sudo /opt/splunk/bin/splunk start
   ```
4. Accept the license and set up an admin username/password.
5. **(Screenshot)**: Show Splunk web login page.

---

## 📥 Log Ingestion

### **Step 2: Add System Logs to Splunk**

To monitor logs like **syslog, auth.log, and kernel logs**, configure Splunk to ingest them:

#### **Using CLI to Add a Monitor**

```bash
sudo /opt/splunk/bin/splunk add monitor /var/log/syslog -index main -sourcetype syslog
```

Repeat for other logs:

```bash
sudo /opt/splunk/bin/splunk add monitor /var/log/auth.log -index main -sourcetype authlog
```

#### **Verify Log Data in Splunk Web UI**

1. Open your browser and navigate to:
   ```
   http://localhost:8000
   ```
2. Log in with your admin credentials.
3. Go to **Search & Reporting** and run:
   ```
   index=main sourcetype=syslog
   ```
4. You should see real-time log data flowing in.
5. **(Screenshot)**: Show logs appearing in the Splunk search UI.

### **Step 3: Set Up Splunk Forwarder**

Splunk Universal Forwarder allows remote log forwarding to the main Splunk instance.

#### **Installing Splunk Forwarder**

1. Download **Splunk Forwarder** from [Splunk Downloads](https://www.splunk.com/en_us/download.html)
2. Install using:
   ```bash
   sudo dpkg -i splunkforwarder*.deb
   ```
3. Enable boot start and start the forwarder:
   ```bash
   sudo /opt/splunkforwarder/bin/splunk enable boot-start
   sudo /opt/splunkforwarder/bin/splunk start
   ```

#### **Configure Forwarding to Splunk**

1. On the Forwarder, add Splunk’s receiver (your main Splunk instance):
   ```bash
   sudo /opt/splunkforwarder/bin/splunk add forward-server <SPLUNK_IP>:9997 -auth admin:password
   ```
2. Add logs for monitoring:
   ```bash
   sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/syslog
   ```
3. On the **main Splunk instance**, enable receiving:
   ```bash
   sudo /opt/splunk/bin/splunk enable listen 9997
   ```
4. **(Screenshot)**: Show successful log forwarding confirmation.

---

## 📊 Log Analysis & Visualization

### **Step 4: Run Security Queries**

#### 🔎 Find Failed SSH Logins:

```spl
index=main sourcetype=authlog "Failed password"
```

#### 🔎 Detect Unauthorized Root Access:

```spl
index=main sourcetype=authlog "session opened for user root"
```

#### 🔎 Monitor System Reboots:

```spl
index=main sourcetype=syslog "systemd" AND "reboot"
```

### **Step 5: Create Dashboards & Alerts**

#### **Creating a Security Dashboard**

1. Go to **Dashboards** in Splunk Web UI.
2. Click **Create New Dashboard**.
3. Add panels for:
   - Failed SSH login attempts.
   - Unauthorized root access.
   - System reboots.
4. **(Screenshot)**: Show dashboard view with visualizations.

#### **Setting Up Alerts**

1. Go to **Search & Reporting**.
2. Run a query, e.g., for multiple failed SSH logins:
   ```spl
   index=main sourcetype=authlog "Failed password" | stats count by user
   ```
3. Click **Save As > Alert**.
4. Set **Trigger Conditions** (e.g., if failed login count > 5 in 5 minutes).
5. Configure **email alerts or webhook notifications**.
6. **(Screenshot)**: Show the alert configuration page.

---

## 🛠️ Challenges & Lessons Learned

- **File Permission Issues**: Resolved with `sudo chmod` for log access.
- **Filtering False Positives**: Fine-tuned queries to reduce noise.
- **Automating Log Ingestion**: Used `cron` jobs for consistent log collection.
- **Forwarder Configuration**: Ensured proper forwarding of logs from remote systems.
- **Alerting Adjustments**: Refined thresholds to minimize unnecessary notifications.

---

## ✅ Conclusion

This project provided hands-on experience in setting up **Splunk for SIEM**, ingesting logs, detecting security threats, and configuring **Splunk Forwarder** for distributed logging. Additionally, it demonstrated creating **alerts and dashboards** to enhance security monitoring.

🔹 **Next Steps**: Expand by integrating firewall logs, IDS/IPS alerts, and cloud security monitoring.

---

**🚀 GitHub Repo:** [Coming Soon]  \
📬 **Contact Me:** [LinkedIn](https://www.linkedin.com/in/emmanuelajayi) | [TryHackMe](https://tryhackme.com/p/EmmySec)

