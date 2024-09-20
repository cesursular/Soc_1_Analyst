### Step 3: Kali Linux for Security Testing

In this step, we will use **Kali Linux** to simulate various attacks and test the security measures put in place with **pfSense**. Kali Linux is a penetration testing and ethical hacking distribution with various tools to test network security and identify vulnerabilities.

### 1. Install Kali Linux

You will need to download and install **Kali Linux** on a virtual machine. This machine will be used to simulate attacks on the pfSense firewall and observe how the system responds, with logs sent to Splunk for analysis.

#### Steps to Install Kali Linux:

- **Download the Kali Linux ISO**:
    - Go to the [Kali Linux website](https://www.kali.org/downloads/) and download the **Kali Linux ISO**.
  
- **Set Up Kali Linux on a Virtual Machine**:
    - Open **VMware Workstation** or **VirtualBox** and create a new virtual machine.
    - **Operating System**: Select Linux (Debian 64-bit).
    - **Memory**: Allocate at least **2GB** of RAM.
    - **Storage**: Allocate at least **20GB** of disk space for Kali Linux.
    - Attach the downloaded **Kali Linux ISO** and follow the installation instructions.
    - Complete the installation and log in to the Kali Linux desktop environment.

### 2. Run Security Tests Against pfSense

Now that Kali Linux is installed, you can use it to perform **security tests** against the pfSense firewall and network. These tests will generate traffic that will be logged in Splunk for analysis.

#### Common Tools and Commands:

1. **Nmap** – Network Scanning:
    - **Nmap** is a network scanning tool that helps you discover open ports and services running on devices behind pfSense.
    - Example command to scan pfSense (replace `192.168.1.1` with pfSense LAN IP):
      ```bash
      nmap -sS 192.168.1.1  # SYN scan
      nmap -sU 192.168.1.1  # UDP scan
      ```
    - Check the firewall logs in Splunk to verify that the scan was logged.

2. **Metasploit** – Vulnerability Testing:
    - **Metasploit** is a powerful tool for vulnerability testing and exploiting potential weaknesses.
    - Example command to start Metasploit:
      ```bash
      msfconsole
      ```
    - Use Metasploit to simulate attacks and test how pfSense handles them.

3. **Hydra** – Brute Force Attack Simulation:
    - **Hydra** is used for simulating brute force attacks on network services (e.g., SSH).
    - Example command for an SSH brute force attack (replace `192.168.1.1` with the target IP):
      ```bash
      hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://192.168.1.1
      ```
    - The attempted brute force login should appear in the Splunk logs.

4. **Ping Flood (ICMP)**:
    - You can use simple **ping** tests to flood the network and observe how pfSense handles high traffic.
    - Example command to initiate a ping flood:
      ```bash
      ping -f 192.168.1.1  # Sends ICMP flood to pfSense IP
      ```

### 3. Monitor and Analyze Traffic in Splunk

Once the tests are running, you can monitor the logs in **Splunk** to see how pfSense processes the traffic. Here’s how to analyze the data:

#### Steps to Analyze Security Logs in Splunk:

1. **Search for Attack Traffic**:
   - In Splunk’s **Search & Reporting** app, you can filter for logs related to your tests:
     ```splunk
     index=pfsense_logs action=block
     ```
   - This will show logs where pfSense has blocked suspicious or malicious traffic (e.g., Nmap scans, brute force attacks).

2. **Create Visualizations**:
   - Use **Splunk’s Visualization tools** to create graphs showing:
     - Volume of incoming attack traffic.
     - Number of blocked connections.
     - Traffic distribution across different ports and protocols.
   
3. **Review Firewall Performance**:
   - Splunk can help you understand how pfSense is performing during high-stress scenarios, like a ping flood or brute force attack.
   - Adjust pfSense firewall rules based on your findings to improve network security.

### 4. Advanced Testing

You can use additional tools in Kali Linux for more advanced testing:
- **Wireshark**: Network packet analysis tool.
- **Nikto**: Web server vulnerability scanner.
- **SQLmap**: SQL injection tool for testing web application security.

---

By following these steps, you will be able to simulate different types of attacks on **pfSense** using **Kali Linux**, generate useful security logs, and analyze the data in **Splunk** for effective monitoring and incident response.