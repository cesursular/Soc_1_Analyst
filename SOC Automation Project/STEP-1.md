## Step 1: Setting Up pfSense

This section explains how to set up **pfSense** in your SOC automation project. It includes installation, configuring the WAN and LAN interfaces, setting up firewall rules, and exporting logs to Splunk.

### 1. Download and Install pfSense on a Virtual Machine

You will first need to download and install pfSense on a virtual machine (VM) using software like **VMware Workstation**, **VirtualBox**, or any other preferred virtualization platform.

#### Steps to Install pfSense:

- **Download pfSense ISO**:
    - Visit [pfSense’s official download page](https://www.pfsense.org/download/) and select:
        - **Architecture**: AMD64 (64-bit)
        - **Installer**: ISO Installer
        - **Mirror**: Choose the closest download mirror.

- **Set Up pfSense in Your Virtual Machine (VM)**:
    - Open **VMware** or **VirtualBox** and create a new virtual machine:
        - **Operating System**: Select FreeBSD 64-bit.
        - **Memory**: Allocate at least 1GB of RAM (depending on your system's resources).
        - **Storage**: Allocate at least 10GB for the pfSense VM.
    - Attach the **pfSense ISO** to the virtual machine.
    - Start the VM and follow the pfSense installation wizard:
        - Select 'Install pfSense' during the boot process.
        - Choose the default keyboard layout and disk partition options.
        - Complete the installation and reboot the VM.

### 2. Configure the WAN and LAN Interfaces

Once pfSense is installed, you will need to configure the **WAN** and **LAN** interfaces.

#### Steps to Configure Interfaces:

- When pfSense boots up, it will automatically try to detect the **WAN** and **LAN** interfaces. Typically:
    - **WAN Configuration (em0)**:
        - If using **DHCP**, pfSense will automatically assign an IP address to the WAN interface.
        - For **Static IP** setups, manually assign an IP address.
    - **LAN Configuration (em1)**:
        - The default LAN IP is `192.168.1.1/24`.
        - You can access pfSense via a web browser by connecting to this IP (e.g., `http://192.168.1.1`).

#### Accessing the Web Interface:

- Open a browser on the host machine or another VM that shares the same LAN subnet.
- Navigate to `http://192.168.1.1`.
- Log in using the default credentials:
    - **Username**: `admin`
    - **Password**: `pfsense`
- Follow the setup wizard to configure the hostname, domain, and DNS server.

### 3. Set Up Firewall Rules to Log Traffic

After configuring the interfaces, create firewall rules to log specific traffic types for monitoring and analysis in Splunk.

#### Steps to Configure Firewall Rules:

- In the **pfSense Web Interface**, go to **Firewall > Rules**.
- Select either the **LAN** or **WAN** tab depending on where you want to control traffic.
- Click **Add** to create a new rule:
    - **Action**: Choose `Pass` or `Block`, depending on what traffic you want to log.
    - **Source**: Define the IP range or network from which the traffic originates (e.g., **LAN subnet** or a specific IP like `192.168.65.132`).
    - **Destination**: Set the destination (e.g., `Any`, `WAN address`, etc.).
    - **Protocol**: Specify whether you want to log **TCP**, **UDP**, or **ICMP** traffic (e.g., for ping requests).
    - **Log Option**: Enable "Log packets that are handled by this rule" to log the traffic.

Once the rules are set up, pfSense will begin logging traffic based on the defined rules.

### 4. Export Logs to Splunk

To analyze firewall logs, export pfSense logs to Splunk via syslog.

#### Steps to Export pfSense Logs to Splunk:

1. **Enable Remote Logging on pfSense**:
    - In the **pfSense Web Interface**, go to **Status > System Logs > Settings**.
    - Scroll down to the **Remote Logging Options** section.
    - Enable the **Send log messages to remote syslog server** option.
    - Enter the IP address of your **Splunk server** in the **Remote log servers** field.
        - Example: `192.168.1.154:514` (assuming Splunk is running on the host machine with IP `192.168.1.154`).
    - Select the log categories you want to forward (e.g., **Firewall events**, **System events**).
    - Save the changes.

2. **Configure Splunk to Receive Logs**:
    - In the **Splunk Web Interface**, navigate to **Settings > Data Inputs > UDP**.
    - Click **New UDP** and set the port to **514** (standard syslog port).
    - Set the **Source Type** to `syslog` and assign an index (e.g., `pfsense_logs`).
    - Save the settings, and Splunk will start receiving logs from pfSense.

3. **Verify the Logs in Splunk**:
    - Go to **Search & Reporting** in Splunk and search for logs from pfSense:
      ```splunk
      index=pfsense_logs sourcetype=syslog
      ```
    - You should now see the logs coming from pfSense, which can be filtered, visualized, and analyzed.

---

By following these steps, you should have pfSense fully installed, configured, and exporting logs to **Splunk** for traffic monitoring and security analysis.
