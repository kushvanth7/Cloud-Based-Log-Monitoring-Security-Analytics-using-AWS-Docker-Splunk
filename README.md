Cloud-Based Log Monitoring & Security Analytics using AWS, Docker & Splunk

This project demonstrates how to deploy Splunk Enterprise on an AWS EC2 instance using Docker, ingest system logs, create security monitoring dashboards, and configure automated alerting for suspicious activity (e.g., SSH failed login attempts).

📌 Project Overview

This project provides a complete workflow for cloud-based log monitoring, security analytics, and alerting using Splunk.
It includes:

Deploying Splunk Enterprise on AWS EC2 with Docker

Ingesting Linux system and authentication logs

Building dashboards to visualize SSH activity, login events, and system operations

Creating real-time alerts for suspicious behavior

End-to-end troubleshooting for Splunk ingestion issues

This project is ideal for Security Operations (SOC), Threat Detection, SIEM learning, and Cloud Security practice.

⚙️ Architecture
Laptop → Upload Logs → Splunk (Docker Container) → Dashboards → Real-Time Alerts
AWS EC2 (Ubuntu) → Docker → Splunk Enterprise

🧰 Tools & Technologies Used
Technology	Purpose
AWS EC2 (Ubuntu)	Cloud hosting for Splunk instance
Docker	Containerized Splunk deployment
Splunk Enterprise	Log ingestion, dashboards, analytics
Linux Logs (syslog, auth.log)	Data source
Email Alerting	Automated notifications
SPL Queries	Dashboard visualizations
🚀 Features Implemented

✔️ Splunk Enterprise deployment on AWS using Docker

✔️ Log ingestion from Linux system (syslog, auth.log)

✔️ Dashboards showing:

SSH failed login attempts

Successful logins

System event monitoring

Time-based security trends

✔️ Email alerts for repeated failed login attempts

✔️ User-uploaded log ingestion for testing

✔️ Handling Splunk permission issues and ingestion troubleshooting

📂 Project Structure
/project
 ├── dashboards/
 │    ├── ssh_failed_attempts.json
 │    ├── user_login_activity.json
 │    └── system_events.json
 ├── sample_logs/
 │    └── syslog.log
 └── README.md

🛠️ Installation & Setup
1. Launch AWS EC2

Ubuntu 22.04

t2.medium recommended

Open ports: 8000, 8088, 22

2. Install Docker
sudo apt update
sudo apt install docker.io -y

3. Run Splunk Container
sudo docker run -d \
 --name splunk \
 -p 8000:8000 \
 -p 8088:8088 \
 -e SPLUNK_START_ARGS="--accept-license" \
 -e SPLUNK_PASSWORD=Admin@123 \
 splunk/splunk:latest

4. Access Splunk
http://<EC2-Public-IP>:8000
Username: admin
Password: Admin@123

5. Upload Logs (for dashboards)

Go to:
Settings → Add Data → Upload → Select syslog.log

This immediately populates dashboards.

📊 Dashboards Created
1. SSH Failed Login Attempts

Detects brute force attempts:

index=main sourcetype=syslog "Failed password"
| stats count by user, src, _time

2. Successful Login Activity
index=main sourcetype=syslog "session opened"
| stats count by user, src

3. System Events Overview
index=main sourcetype=syslog
| timechart count by host

🔔 Alerts Configured

Alert: Multiple failed SSH login attempts

index=main "Failed password"
| stats count by src
| where count > 3


Action: Send email notification

📘 Learning Outcomes

Deploying enterprise SIEM (Splunk) in cloud

Building dashboards & SPL search queries

Detecting authentication attacks

Real-time alerting for security events

Troubleshooting Docker & Splunk ingestion issues

📜 License

This project is for educational & demonstration purposes only.
