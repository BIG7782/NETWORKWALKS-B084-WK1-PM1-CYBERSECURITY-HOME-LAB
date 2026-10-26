# 🔐 Personal Cybersecurity Lab Setup

Building an isolated virtual lab for cybersecurity, penetration testing, and ethical hacking practice.

## 📌 Project Overview

This project focuses on setting up a virtual cybersecurity and penetration-testing laboratory using Oracle VirtualBox and Kali Linux.

The purpose of the lab is to create a controlled environment where virtualization, Linux administration, network configuration, reconnaissance, vulnerability assessment, packet analysis, and security-testing activities can be practiced safely.

The lab uses a VirtualBox NAT Network to allow connected virtual machines to communicate with one another while providing outbound network connectivity. Additional target machines can be added in future projects for authorized security testing.

## 🎯 Objectives

The main objectives of this project are to:

- Install and configure Oracle VirtualBox.
- Extract and import Kali Linux into VirtualBox.
- Create a dedicated NAT Network for the cybersecurity lab.
- Configure network connectivity for the Kali Linux virtual machine.
- Configure and verify IPv4 addressing and routing.
- Test gateway connectivity and DNS resolution.
- Create a clean virtual machine snapshot.
- Document the complete lab setup, screenshots, and verification process.
- Prepare the environment for future cybersecurity projects.

## 🛡️ Purpose of the Lab

The lab provides a controlled environment for cybersecurity education and authorized security testing.

It can be used for:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web application security testing
- Linux administration practice
- Ethical hacking exercises
- Cybersecurity tool experimentation

⚠️ **Important:** Use this laboratory only on systems you own or have explicit permission to test. A NAT Network does not guarantee complete isolation from the host or external networks. Verify network boundaries before conducting security tests.

## 🏗️ Lab Architecture

```text
                  HOST COMPUTER
                  Windows 10
                       |
               Oracle VirtualBox
                    Version 7.2
                       |
                VirtualBox NAT Network
                    10.0.0.0/24
                       |
                +------+------+
                |             |
           Kali Linux     Future Lab VM
           10.0.0.2*      10.0.0.x*
                |             |
                +------+------+
                       |
             VM-to-VM Communication
              and Outbound NAT Access
```

\* Example addresses. Verify the actual network configuration on your system.

Additional authorized target machines can be connected to the same NAT Network in future projects.

## ⚙️ Lab Configuration

| Component | Configuration |
|---|---|
| Host Operating System | Windows 10 |
| Host RAM | 6 GB |
| Processor | Intel Core i3 |
| Hypervisor | Oracle VirtualBox 7.2 |
| Security Operating System | Kali Linux 2026.2 |
| Kali Linux RAM | 2048 MB |
| Virtual Network | NAT Network |
| Network Name | NatNetwork |
| Network Prefix | 10.0.0.0/24 |
| Kali Linux IP Address | 10.0.0.2/24 |
| Default Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |
| Future VM Address Range | 10.0.0.3–10.0.0.99 |

**Note:** These values describe the intended configuration. Verify them against your actual VirtualBox settings and Kali Linux network configuration. Ensure that static IP addresses do not conflict with the DHCP address pool.

## 🪜 Lab Setup Procedure

### Step 1. Install 7-Zip

7-Zip is used to extract the Kali Linux virtual machine files from the downloaded archive.

**Download:**

[Official 7-Zip Website](https://www.7-zip.org/download.html)

### Step 2. Install Oracle VirtualBox

Oracle VirtualBox is used as the hypervisor to create, configure, and manage virtual machines for the cybersecurity lab.

**Download:**

[Official VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads)

### Step 3. Create the NAT Network

Open VirtualBox and create a dedicated NAT Network for the cybersecurity lab.

Configure the network as follows:

```text
Network Name: NatNetwork
IPv4 Prefix:  10.0.0.0/24
DHCP:         Enabled
IPv6:         Disabled
```

A NAT Network allows multiple virtual machines connected to the same network to communicate with each other while supporting outbound connectivity through network address translation.

**Screenshot:** `vm-settings.png`

### Step 4. Import Kali Linux

Download Kali Linux from the official Kali Linux website and import the virtual machine into VirtualBox.

**Download:**

[Official Kali Linux Downloads](https://www.kali.org/get-kali/)

Configure the virtual machine's network adapter as follows:

```text
Adapter:      Adapter 1
Attached to:  NAT Network
Network:      NatNetwork
Adapter Type: Intel PRO/1000 MT Desktop
RAM:          2048 MB
```

A shared folder was also configured to transfer required files between the host operating system and the Kali Linux virtual machine.

**Screenshot:** `3-screenshot-kali-linux.png`

### Step 5. Configure the Kali Linux Network

Check the network interfaces and assigned IP addresses using:

```bash
ip -br addr
```

Check the routing table:

```bash
ip route
```

The intended network configuration is:

```text
IP Address:   10.0.0.2
Subnet Mask:  255.255.255.0
Gateway:      10.0.0.1
DNS Server:   8.8.8.8
```

**Screenshot:** `4-screenshot-kali-network-settings.png`

Because DHCP is enabled, confirm that the intended IP address is available and does not conflict with another virtual machine. Use a DHCP reservation or an appropriate static configuration if required.

### Step 6. Verify Network Connectivity

After configuring the network, verify the IP address, routing, gateway connectivity, DNS resolution, and outbound connectivity.

#### 6.1 Check the IP address

```bash
ip -br addr
```

This command displays the network interfaces and their assigned IP addresses.

#### 6.2 Check the routing table

```bash
ip route
```

This command displays the routing table and default gateway.

#### 6.3 Test gateway connectivity

Replace the example address with the actual gateway address if it differs.

```bash
ping -c 4 10.0.0.1
```

#### 6.4 Test outbound connectivity

```bash
ping -c 4 8.8.8.8
```

A successful response indicates that ICMP connectivity to the destination is available. Failure alone does not necessarily mean internet access is unavailable.

#### 6.5 Verify DNS resolution

```bash
getent hosts kali.org
```

This command checks whether the system can resolve the hostname.

**Screenshot:** `network-verification.png`

Record the actual test results and any troubleshooting performed. Mark tests as successful only after verifying the results.

### Step 7. Create a Clean VM Snapshot

After completing the initial configuration and verification, create a snapshot using VirtualBox Snapshot Manager.

Example snapshot name:

```text
Clean Kali - Lab Setup
```

A clean snapshot provides a known recovery point before making significant changes or conducting authorized security exercises.

## 🔎 Lab Verification

| Test | Command | Expected Result |
|---|---|---|
| Check IP address | `ip -br addr` | Assigned IP address is displayed |
| Check routing | `ip route` | Routing table and default route are displayed |
| Test gateway | `ping -c 4 10.0.0.1` | Replies if the gateway responds to ICMP |
| Test outbound connectivity | `ping -c 4 8.8.8.8` | Replies if ICMP connectivity is available |
| Test DNS resolution | `getent hosts kali.org` | Hostname resolves to an IP address |
| Verify Nmap | `nmap --version` | Installed Nmap version is displayed |

These are verification procedures and expected results, not a claim that every test has already succeeded.

## 💡 What I Learned

Through this project, I learned how to:

- Create a virtual cybersecurity laboratory using Oracle VirtualBox.
- Import and configure a Kali Linux virtual machine.
- Configure a VirtualBox NAT Network.
- Understand the difference between NAT and NAT Network.
- Inspect IPv4 addresses, subnet masks, gateways, and DNS settings.
- Use Linux commands to verify network connectivity.
- Troubleshoot basic virtual networking issues.
- Create virtual machine snapshots for recovery.
- Document technical configurations and screenshots using GitHub.
- Prepare a foundation for future cybersecurity and penetration-testing exercises.

## 🔐 Security and Ethical Use

This laboratory is intended strictly for educational purposes and authorized security testing.

- Test only systems you own or have explicit permission to assess.
- Use controlled lab targets for vulnerability assessment and testing.
- Verify network boundaries before running security tools.
- Create snapshots before significant system changes.
- Document findings and remediation steps responsibly.
- Avoid testing public or third-party systems without authorization.

## 🔗 Tools and Resources

- **7-Zip:** [Official Download](https://www.7-zip.org/download.html)
- **Oracle VirtualBox:** [Official Downloads](https://www.virtualbox.org/wiki/Downloads)
- **Kali Linux:** [Official Downloads](https://www.kali.org/get-kali/)

## 👤 Author

**Bigyan Tamang**

Cybersecurity Learner | Network and System Administration

LinkedIn: [Bigyan Tamang](https://www.linkedin.com/in/bigyan-tamang-776613200/)

## 📌 Project Information

- **Program:** Cybersecurity at NetworkWalks
- **Batch:** B084
- **Week:** 01
- **Project:** Cybersecurity and Penetration-Testing Lab Setup
- **Environment:** Oracle VirtualBox and Kali Linux
- **Network:** 10.0.0.0/24
- **Repository:** `NETWORKWALKS-B084-WK1-PM1-CYBERSECURITY-HOME-LAB`

---

*This repository documents my hands-on cybersecurity learning journey, including virtualization, network configuration, Linux administration, lab verification, screenshots, and ethical security testing.*
