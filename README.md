# SOC-Azure-Sentinal-NGFW-Project
# SOC Automation with Azure, Sentinel, and Fortinet

This project demonstrates the setup of a Security Operations Center (SOC) environment using **Azure**, **Microsoft Sentinel**, and a **Fortinet Fortigate Next-Gen Firewall**. It highlights expertise in cloud security, network automation, and threat monitoring/response.


## Project Overview
The goal is to automate a SOC setup with Azure as the cloud platform, Fortinet for network security, and Sentinel for threat detection and incident response, simulating a real-world security environment.

## Step-by-Step Setup

### 1. Set Up Azure Account and Dashboard
- **Task**: Configure an Azure subscription and create a resource group with a monitoring dashboard.
- **Procedure**:
  - Log into Azure Portal with your credentials.
  - Create a resource group (e.g., `SOC-Project`) in a region like `central-india` for centralized management.
  - Build a custom dashboard in the portal, adding tiles for VM status, network traffic, and firewall metrics.
- **Skills**: Azure resource management, dashboard customization.

### 2. Create Log Analytic Workspace
- **Task**: Establish a workspace to collect and analyze logs from various sources.
- **Procedure**:
  - In Azure Portal, navigate to Log Analytics Workspaces and create one (e.g., `SOC-Workspace`).
  - Link it to `SOC-Project` and select `central-india` for consistency.
  - Enable basic log retention (e.g., 30 days) for analysis.
- **Skills**: Log management, Azure analytics setup.

### 3. Deploy Microsoft Sentinel
- **Task**: Activate Sentinel as the SIEM for security monitoring and threat detection.
- **Procedure**:
  - In Azure Portal, go to Microsoft Sentinel and attach it to `SOC-Workspace`.
  - Configure initial settings, such as enabling the Syslog connector for future log ingestion.
  - Verify the workspace is active in Sentinel’s overview page.
- **Skills**: SIEM deployment, security orchestration.

### 4. Create Two Subnets
- **Task**: Segment a Virtual Network (VNet) into two subnets for isolated traffic.
- **Procedure**:
  - Create a VNet (e.g., `SOC-VNet`) with address space `10.0.0.0/16` in `SOC-RG`.
  - Add `Subnet1` (`10.0.1.0/24`) for the firewall and `Subnet2` (`10.0.2.0/24`) for VMs using the portal or CLI.
  - Ensure subnets are associated with the VNet routing table.
- **Skills**: Network segmentation, Azure networking.

### 5. Deploy Fortinet Fortigate NGFW
- **Task**: Deploy a Fortinet Next-Gen Firewall in Azure for network protection.
- **Procedure**:
  - From Azure Marketplace, select the Fortigate VM (single instance) and deploy it to `Subnet1`.
  - Assign a static IP (e.g., `10.0.1.4`) and configure public/private NICs.
  - Log into FortiOS, upload your license, and verify connectivity.
- **Skills**: Firewall deployment, cloud integration.

### 6. Deploy Two Virtual Machines
- **Task**: Provision VMs to simulate a network environment for testing.
- **Procedure**:
  - Deploy `VM1` in `Subnet1` and `VM2` in `Subnet2` using Ubuntu LTS via Azure Portal.
  - Set VM sizes (e.g., `Standard_B1s`), configure SSH access, and assign private IPs.
  - Test ping between VMs to confirm network setup.
- **Skills**: VM provisioning, Azure compute.

### 7. Initial Configuration of the Firewall
- **Task**: Perform basic setup on the Fortigate firewall.
- **Procedure**:
  - SSH into Fortigate using its IP (e.g., `10.0.1.4`).
  - Set the hostname to `SOC-Fortigate` and configure `port1` with IP `10.0.1.4/24`.
  - Save and reboot to apply changes.
- **Skills**: Firewall administration, CLI usage.

### 8. Configure Firewall Rules
- **Task**: Define policies to control traffic between subnets.
- **Procedure**:
  - In FortiOS, create a policy allowing traffic from `Subnet1` (source: `all`) to `Subnet2` (destination: `all`).
  - Set service to `ALL` and enable logging for monitoring.
  - Apply the policy and verify it’s active.
- **Skills**: Security policy creation, traffic management.

### 9. Enable IPS and Apply to Rules
- **Task**: Activate Intrusion Prevention System (IPS) for threat protection.
- **Procedure**:
  - In FortiOS, enable the `default` IPS sensor under Security Profiles.
  - Edit the existing firewall policy to include the IPS sensor.
  - Test by generating suspicious traffic (e.g., malformed packets) and check logs.
- **Skills**: Threat prevention, IPS configuration.

### 10. Test Connectivity with Brute Force Simulation
- **Task**: Validate firewall and IPS by simulating an attack.
- **Procedure**:
  - From `VM1`, run a controlled SSH brute-force script targeting `VM2` (e.g., 20 attempts).
  - Check Fortigate logs for blocked attempts and IPS alerts.
  - Ensure no unauthorized access occurs.
- **Skills**: Security testing, log analysis.

### 11. Connect Firewall to Log Analytic Workspace and Sentinel
- **Task**: Forward Fortinet logs to Azure for centralized monitoring.
- **Procedure**:
  - In FortiOS, configure Syslog to send CEF-formatted logs to the Log Analytics Workspace IP.
  - In Sentinel, enable the CEF via AMA connector and map Fortigate logs.
  - Validate log ingestion in the workspace query editor.
- **Skills**: Log forwarding, SIEM integration.

### 12. Create Alerts and Incident Response in Sentinel
- **Task**: Build alerts and automate responses for security incidents.
- **Procedure**:
  - In Sentinel, create an analytic rule (e.g., detect >10 failed SSH attempts in 5 minutes from `Syslog`).
  - Set severity to `Medium` and link a playbook (e.g., send email via Logic Apps).
  - Simulate an incident with the brute-force test and review the generated alert/incident.
- **Skills**: Alert creation, automation, incident response.

## Skills Demonstrated
- **Cloud Security**: Azure resource deployment and management.
- **Network Security**: Subnetting, firewall setup, and IPS.
- **Automation**: Resource orchestration and log integration.
- **Threat Monitoring**: SIEM deployment, alert configuration, and incident response.

## Tools Used
- Azure Portal/CLI
- Fortinet FortiOS
- Microsoft Sentinel
- Log Analytics Workspace
- Ubuntu VMs

---
