<div align="center">

## 🔐 Cybersecurity Lab Setup - VirtualBox & Kali Linux

![Cybersecurity](https://img.shields.io/badge/SKILL-CYBERSECURITY-lightgrey?style=for-the-badge)
![VirtualBox](https://img.shields.io/badge/VER-VIRTUALBOX%20V7.2-blue?style=for-the-badge)
![Kali](https://img.shields.io/badge/KALI%20LINUX-V2026.2-black?style=for-the-badge)
![Linux](https://img.shields.io/badge/SKILL-LINUX-red?style=for-the-badge)
![Network](https://img.shields.io/badge/NETWORK-10.0.0.0%2F24-black?style=for-the-badge)

![Virtualization](https://img.shields.io/badge/SKILL-VIRTUALIZATION-red?style=for-the-badge)
![GitHub](https://img.shields.io/badge/GITHUB-100000?style=for-the-badge&logo=github&logoColor=white)
![Kali Linux](https://img.shields.io/badge/KALI%20LINUX-557C94?style=for-the-badge)
![NetworkWalks](https://img.shields.io/badge/NETWORKWALKS-lightgrey?style=for-the-badge)
![Ethical](https://img.shields.io/badge/ETHICAL%20HACKING-orange?style=for-the-badge)
![Batch](https://img.shields.io/badge/BATCH-B084-blueviolet?style=for-the-badge)

</div>

## 🚀 Overview
This is my Week 01 Project for NetworkWalks (Batch B084). I built a safe, isolated cybersecurity lab using VirtualBox and Kali Linux on my personal laptop. The lab is fully private and separated from my main network.

## 🎯 Objectives
These are the main goals I completed in this week:
* Install Oracle VirtualBox on my Windows 11 host
* Import and setup Kali Linux VM
* Create a private NAT Network for isolation
* Give a permanent static IP to Kali (10.0.0.2)
* Verify gateway, internet and DNS is working
* Take a clean snapshot as backup
* Document the full process for future labs

## 🛡️ Purpose of the Lab
I built this lab to learn cybersecurity practically without risking my real network. This isolated lab will be used for:
* Learning basic Linux and networking commands
* Network scanning and footprinting with nmap
* Checking open ports and services
* Understanding how NAT Network works
* Practicing safely before moving to vulnerable target VMs in Week 2

> This lab is only for learning on my own VMs. Not for scanning public networks.

## 🏗️ Lab Architecture
This is how my lab looks. My Kali VM is connected to the private NatNetwork (10.0.0.0/24) which is separate from my main WiFi.

<img width="1915" height="887" alt="Screenshot 2026-10-26 172408" src="https://github.com/user-attachments/assets/52ac1022-27dd-4802-a491-a0b80219d622" />

**My Laptop Specs:**
* Host OS: Windows 11
* CPU: Intel Core i3-1315U @ 1.20GHz
* RAM: 8GB
* Storage: 512GB SSD
* Hypervisor: VirtualBox v7.2
* Guest OS: Kali Linux 2026.2 (2048MB RAM)

## 🛠️ Setup Guide

### Step 1. Install 7-Zip
I installed 7-Zip to extract the Kali Linux VM files which were in .7z format.
* Downloaded from 7-zip.org
* Installed and extracted Kali folder to my D: drive.

### Step 2. Install VirtualBox
Installed Oracle VirtualBox v7.2 on my Windows 11 host.
* Enabled all network adapter drivers during installation.
* Checked File > Tools > Network Manager is working.

### Step 3. Create the NAT Network
This is the most important step. This creates the private switch for my lab.

<img width="1917" height="376" alt="Step 3 - NAT Network List" src="https://github.com/user-attachments/assets/520d8fdb-dce8-4442-82b1-0e202cb21b38" />

<img width="867" height="505" alt="Step 3 - NatNetwork Details" src="https://github.com/user-attachments/assets/93db3a7c-9bb4-44fd-8e48-59a6e7293575" />

* Go to: VirtualBox > File > Tools > Network Manager > NAT Networks > Create
* **Network Name:** NatNetwork
* **IPv4 Prefix:** 10.0.0.0/24
* **DHCP:** Enabled
* **IPv6:** Disabled

### 4. Shared Folder & Clipboard Configuration (As per requirements)

As per the lab requirement: Shared folders should be enabled with /downloads folder shared from host machine.

**Configuration:**
- **Host Path:** `C:\Users\rmnad\Downloads`
- **Guest Mount:** `/downloads`
- **Settings:** VirtualBox > Settings > Shared Folders > Add > Auto-mount enabled
- **Verification:** Inside Kali, run `ls /downloads` and `df -h | grep downloads`

**Clipboard & Drag/Drop:**
- Settings > General > Advanced > Shared Clipboard: Bidirectional
- Drag'n'Drop: Bidirectional
- This allows easy file transfer between Host (Windows) and Kali VM.

<img width="522" height="452" alt="Screenshot 2026-10-25 221536" src="https://github.com/user-attachments/assets/aad6cedd-770c-4769-8718-c597be25bc69" />
<img width="1197" height="300" alt="Screenshot 2026-10-26 182243" src="https://github.com/user-attachments/assets/d34c286a-8426-4d88-9951-3ed37a4a043f" />

### Step 5. Import Kali Linux
1. Double-clicked the Kali `.vbox` file to import into VirtualBox.
2. Settings > System > Motherboard > RAM: 2048 MB
3. Settings > Network > Adapter 1 > Attached to: NAT Network, Name: NatNetwork
4. Adapter Type: Intel PRO/1000 MT Desktop (default)
5. Enabled Bidirectional Clipboard and Drag & Drop.

### Step 6. Configure the Kali Linux Network
This is where I set the static IP as per Sir's video.

**My IP Config:**
* Address: 10.0.0.2
* Netmask: 24 (255.255.255.0)
* Gateway: 10.0.0.1
* DNS: 10.0.0.1 (Sir's video config)

**Commands I used in Kali Terminal:**

```bash
# Check current IP
ip a

# Set static IP permanently
sudo nmcli con mod "Wired connection 1" ipv4.addresses 10.0.0.2/24 ipv4.gateway 10.0.0.1 ipv4.dns 10.0.0.1 ipv4.method manual

# Apply the changes
sudo nmcli con down "Wired connection 1" && sudo nmcli con up "Wired connection 1"

# Verify
ip a
```

### Step 7. Create a Clean VM Snapshot
After everything worked, I shut down Kali properly and took a clean snapshot.

- VirtualBox > Select Kali VM > Snapshots > Take
- Name: My First Kali Linux
- Description: My first lab setup with network 10.0.0.2 working

<img width="1768" height="881" alt="Screenshot 2026-10-26 110728" src="https://github.com/user-attachments/assets/bebd98dd-9988-4b86-9482-6fd8d80dc6e2" />

### My Lab Architecture - Running
After all steps, my lab is running. You can see sf_Downloads shared folder is working.

<img width="1767" height="812" alt="My Lab Running" src="https://github.com/user-attachments/assets/f955112b-c910-4196-807b-523dc1ddf77b" />

| Device | IP | Gateway | Purpose |
| :--- | :--- | :--- | :--- |
| Gateway | 10.0.0.1 | - | VirtualBox Router |
| Kali (Me) | 10.0.0.2 | 10.0.0.1 | Attacker Machine |
| Future Targets | 10.0.0.3-99 | 10.0.0.1 | For vulnerable VMs |


## 🔎 Lab Verification
I verified the lab after taking the snapshot.

**1. Gateway Connectivity Test (10.0.0.1):**
Ping to gateway is successful.

<img width="616" height="158" alt="Screenshot 2026-10-26 171921" src="https://github.com/user-attachments/assets/4d035166-69ce-408a-8a1c-52126cc58145" />

**2. Internet Connectivity Test (8.8.8.8):**
Ping to internet is successful.

<img width="606" height="206" alt="Screenshot 2026-10-26 172002" src="https://github.com/user-attachments/assets/31b9516a-2908-403b-92f3-551ba6946f98" />

**3. DNS Test - My Result:**

<img width="1085" height="330" alt="Verification - nslookup" src="https://github.com/user-attachments/assets/da52941c-84dc-45ee-95e0-0ed62da314fa" />

**My Final Results:**
IP Address: 10.0.0.2/24
Gateway: 10.0.0.1
DNS: 10.0.0.1
Ping Gateway: 2 packets received, 0% loss
Ping Internet: 2 packets received, 0% loss
Status: LAB READY

## 🐞 Problems Encountered & Solutions

1. Couldn't find NAT Network option
   Problem: I was searching in Settings > Network.
   Solution: Correct path is File > Tools > Network Manager > NAT Networks.

2. Got error nmcli not found
   Problem: Spelling mistake.
   Solution: Correct command is nmcli.

3. Didn't know what ~ means in terminal.
   Problem: Thought I need to type ~.
   Solution: ~ just means Home folder.

4. ls /media/sf_downloads said No such file
   Problem: Linux is case-sensitive!
   Solution: Correct is sf_Downloads with capital D.

5. Internet not working after static IP
   Problem: DNS set to 8.8.8.8 was slow.
   Solution: Changed DNS to 10.0.0.1 as per Sir's video.

## 💡 What I Learned
Through this Week 01 project, I built my first cybersecurity lab from scratch.

**1. NAT vs NAT Network**
I learned that standard NAT only allows a single VM to access the internet. A NAT Network allows multiple VMs on the same network (like 10.0.0.2, 10.0.0.3) to talk to each other while still having internet access. This is perfect for a future pentesting lab.

**2. Virtual Machine Networking**
I understood how VirtualBox network adapters work and how to set up communication between VMs and the host.

**3. Static IP Configuration**
I learned how to set a permanent static IP (10.0.0.2/24) in Kali Linux using terminal commands (`nmcli`) and verify it with `ip a`, `ping`, and `nslookup`.

**4. VM Snapshots**
I learned the importance of taking a clean snapshot before doing any risky experiments. My snapshot `My First Kali Linux` is my safe restore point.

**5. Documentation**
I learned that documenting every command, screenshot, problem, and solution is a key skill for a cybersecurity professional.

## 🔐 Security & Ethical Use
This lab is built strictly for educational purposes. I will only use it to test my own VMs inside the 10.0.0.0/24 network. I will not use it to attack any public or unauthorized systems.

## 🔗 Tools & Resources
- 7-Zip: https://www.7-zip.org/
- VirtualBox: https://www.virtualbox.org/
- Kali Linux: https://www.kali.org/get-kali/

## 👤 Author
**R.M.Naduni Umeda - Batch B084**
Cybersecurity Student at NetworkWalks

## 📌 Project Info
- Program: Cybersecurity at NetworkWalks
- Week: 01
- Project: Cybersecurity & Pentesting Lab Setup
- Status: LAB READY - Ready for Week 02
