### Step 2: Setting Up Splunk

In this section, we will guide you through setting up **Splunk** to collect and analyze logs from **pfSense**. Splunk acts as the central log management and SIEM platform in this SOC automation project.

### 1. Download and Install Splunk

#### Steps to Download and Install Splunk:

- **Download Splunk**:
  - Go to [Splunk's official website](https://www.splunk.com/en_us/download.html) and download the **Free Splunk Enterprise** version for your operating system.
  - You can also opt for **Splunk Universal Forwarder** if you plan to collect logs from multiple sources or systems.
  
- **Install Splunk**:
  - Follow the installation instructions based on your operating system:
    - **Linux**: Follow the instructions for installing via `.deb` or `.rpm` package.
    - **Windows**: Run the installer and follow the setup wizard.
  - Set up an admin username and password during the installation.

- **Start Splunk**:
  - After installation, start the Splunk service using the following commands:
    - **Linux**:
      ```bash
      sudo /opt/splunk/bin/splunk start
      ```
    - **Windows**: Start Splunk from the Start Menu.
  - Once Splunk is running, access it by opening a web browser and navigating to:
    - `http://localhost:8000` (replace `localhost` with your IP address if on a remote server).
  
  - Log in with the admin credentials you created during the setup.

### 2. Configure Data Inputs to Receive Logs from pfSense

#### Steps to Configure Data Inputs:

1. **Open the Splunk Web Interface**:
   - Navigate to `http://<splunk_ip>:8000` and log in as the **admin** user.

2. **Set Up a Syslog Data Input**:
   - Go to **Settings > Data Inputs > UDP** and click **Add New**.
   - Set the **Port** to **514** (the standard syslog port).
   - **Source Type**: Set this to `syslog`.
   - **Index**: Create or select an index (e.g., `pfsense_logs`).

3. **Save and Enable the Input**:
   - Save the settings, and ensure the input is enabled to start receiving logs from pfSense.

### 3. Create Dashboards for Traffic Analysis

Once Splunk is receiving logs from pfSense, you can create **dashboards** to visualize network traffic and security events.

#### Steps to Create a Dashboard:

1. **Go to the Splunk Search & Reporting App**:
   - In the top menu, click on **Search & Reporting**.

2. **Search for pfSense Logs**:
   - Use the following Splunk query to search for pfSense logs:
     ```splunk
     index=pfsense_logs sourcetype=syslog
     ```

3. **Create Visualizations**:
   - Use Splunk’s **Visualization** tools to create charts, graphs, and tables that show:
     - Blocked vs. allowed traffic.
     - Traffic by protocol (TCP, UDP, ICMP).
     - Source and destination IPs.
   
4. **Save the Dashboard**:
   - Once you create the necessary visualizations, save the dashboard for easy access to traffic and security event insights.

### 4. Set Up Alerts for Security Incidents

Splunk can also be configured to send **alerts** based on specific conditions, such as suspicious traffic patterns or blocked attacks.

#### Steps to Set Up Alerts:

1. **Go to the Alerts Section**:
   - In the **Search & Reporting** app, go to the **Alerts** section.

2. **Create a New Alert**:
   - Click **New Alert** and define the search criteria for suspicious traffic.
   - Example search query for blocked traffic:
     ```splunk
     index=pfsense_logs action=block
     ```

3. **Configure the Alert**:
   - Set up conditions, such as the number of blocked packets in a given time frame.
   - Choose how you want to be notified (e.g., email or Slack).

4. **Save the Alert**:
   - Save the alert, and Splunk will notify you whenever the conditions are met.

---

By following these steps, you will have **Splunk** configured to receive, visualize, and analyze logs from **pfSense**, allowing for detailed traffic monitoring and security event management.