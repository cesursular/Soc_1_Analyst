# SOC Automation Project

## Overview
This project sets up a basic Security Operations Center (SOC) with automated monitoring and log management using **pfSense**, **Splunk**, **Kali Linux**, and **CyberOps**. The project focuses on automating incident detection and response through log analysis.

### Technologies Used:
- **pfSense**: Network firewall and router.
- **Splunk**: Log management and SIEM solution.
- **Kali Linux**: Offensive security testing and simulation.
- **CyberOps**: Security operations and testing tools.

## Setup Instructions

### Prerequisites:
1. **VMware Workstation/VirtualBox**: To run the virtual machines.
2. **pfSense ISO**: Download from [pfSense Official Site](https://www.pfsense.org/download/).
3. **Splunk Free Version**: Download from [Splunk](https://www.splunk.com/en_us/download.html).

### Step 1: Setting Up pfSense
1. Download and install pfSense on a virtual machine.
2. Configure the WAN and LAN interfaces.
3. Set up firewall rules to log traffic.
4. Export logs to Splunk.

### Step 2: Setting Up Splunk
1. Install Splunk on a virtual machine.
2. Set up data inputs for syslog from pfSense (UDP 514).
3. Create a dashboard to monitor incoming traffic and alerts.

### Step 3: Testing with Kali Linux
1. Use Nmap and other tools from Kali Linux to simulate attacks.
2. Monitor and analyze attacks in Splunk.

### Step 4: CyberOps Security Tools
1. Configure additional testing and automation tools on CyberOps VM.
2. Test response to different scenarios (e.g., brute force attacks).

### Troubleshooting
- If you encounter issues with Splunk not receiving logs, check firewall settings on both pfSense and the host machine.

## Contributors
- CESUR SULAR - Project Lead - Security Analyst
