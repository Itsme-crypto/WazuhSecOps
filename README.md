# WazuhSecOps
A scalable solution built on Wazuh for continuous monitoring, real-time threat detection, and improving overall security posture.
# Wazuh System Monitoring Implementation
This repository documents the process of setting up Wazuh, an open-source security monitoring platform, to monitor and analyze security events on my system. The goal of this project is to demonstrate my ability to implement a real-time monitoring system using Wazuh for intrusion detection, log analysis, and system security management.

# Table of Contents
+ Introduction
+ Prerequisites
+ Installation Steps
+ Wazuh Configuration
+ Integration with Kibana
+ Monitoring Logs and Alerts
+ Troubleshooting
+ Conclusion
+ License

# Introduction
Wazuh is an open-source security information and event management (SIEM) tool that provides comprehensive log analysis, intrusion detection, and monitoring capabilities. This project aims to set up Wazuh on my system for security event monitoring, allowing for the detection of unauthorized access attempts, system changes, and other potential security threats.
# Prerequisites
Before starting, ensure the following prerequisites are met:

+ A Linux-based system (Ubuntu 20.04 or later recommended)
+ Root or sudo privileges for installing software
+ A basic understanding of Linux command-line operations
+ Internet connection for downloading packages

Software dependencies:

+ Wazuh Manager for managing agents and processing security events.
+ Elasticsearch, Logstash, and Kibana for storing, processing, and visualizing logs.

# Installation Steps
### 1. Install Wazuh Manager

- First, install the necessary dependencies and Wazuh Manager:

```bash
sudo apt update
sudo apt install -y curl apt-transport-https lsb-release gnupg 
```

- Add the Wazuh repository and GPG key:
```bash
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo apt-key add -
sudo sh -c 'echo "deb https://packages.wazuh.com/4.x/apt/ stable main" > /etc/apt/sources.list.d/wazuh.list'
sudo apt update
```
- Now, install Wazuh Manager:
```bash
sudo apt install wazuh-manager
```
- Enable and start Wazuh Manager:
 ```bash
sudo systemctl enable wazuh-manager
sudo systemctl start wazuh-manager
 ```
- Verify Wazuh Manager is running:
 ```bash
sudo systemctl status wazuh-manager
```
### 2. Install the Wazuh Agent (if monitoring multiple systems)
```bash
sudo apt install wazuh-agent
```
### 3. Configure Wazuh Manager
Edit the ossec.conf file to configure log monitoring:
```bash
sudo vi /var/ossec/etc/ossec.conf
```
Here, you can define which logs to monitor, such as syslog, authentication logs, and more.

# Wazuh Configuration
After installation, you need to configure the Wazuh Manager and agents:

### 1. Configure Log Monitoring:
Modify the ossec.conf file to specify which logs you want to monitor:
```xml
<localfile>
    <log_format>syslog</log_format>
    <location>/var/log/syslog</location>
</localfile>
```
### 2. Start Wazuh Manager:    
Restart the Wazuh Manager for the changes to take effect:
```bash
sudo systemctl restart wazuh-manager
```
### 3. Verify Logs:
To verify that Wazuh is processing logs, use the following command:
```bash
sudo tail -f /var/ossec/logs/ossec.log
```
# Integration with Kibana
Wazuh integrates seamlessly with the Elastic Stack (Elasticsearch, Logstash, Kibana) for better visualization and reporting of security data.
### 1. Install the Wazuh Kibana Plugin
```bash
sudo bin/kibana-plugin install https://github.com/wazuh/wazuh-kibana-app/releases/download/v4.x.x/wazuhapp-x.x.x.zip
```
### 2. Configure Kibana    
Once the plugin is installed, ensure Kibana is connected to Elasticsearch and is ready to visualize Wazuh alerts. You may need to edit the wazuh.yml file to set up the connection.
### 3. Access Kibana Dashboard
You can now access the Kibana dashboard by navigating to:
```bash
http://<KIBANA_SERVER_IP>:5601/app/wazuh
```
Here, you can view security alerts, historical data, and real-time events.

# Monitoring Logs and Alerts
With Wazuh set up, you can start monitoring your system for suspicious activity. Examples of logs monitored include:

- Authentication logs (e.g., failed login attempts)
- System logs (e.g., changes in system configuration)
- Application logs (e.g., web server logs)

You can view security alerts and logs through the Kibana dashboard, or by using the following command to see them directly in the terminal:
```bash
sudo tail -f /var/ossec/logs/alerts/alerts.json
```
# Troubleshooting
Here are some common issues and solutions:
### 1. Wazuh Manager not starting

Check logs using:
```bash
sudo journalctl -u wazuh-manager
```
Ensure all dependencies are installed and no conflicting services are running.

### 2. Kibana not displaying Wazuh data

- Verify the Wazuh Kibana plugin is installed correctly.
- Ensure Kibana is connected to Elasticsearch and the Wazuh index is available.
  
# Conclusion  
By implementing Wazuh for system monitoring, you've created a powerful and scalable security solution for your system. Integrating it with the Elastic Stack provides a complete monitoring and alerting framework, offering real-time visibility into potential threats.

This project not only improves system security by detecting intrusions and anomalies but also deepens your understanding of security monitoring and intrusion detection systems. With Wazuh, you’ve established a foundation for a proactive security posture, enabling quick identification and response to security incidents.

This implementation showcases your ability to set up, configure, and maintain a comprehensive security solution — an essential skill for a cybersecurity professional.


