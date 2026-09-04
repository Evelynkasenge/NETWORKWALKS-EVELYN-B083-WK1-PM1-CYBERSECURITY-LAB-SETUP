# NETWORKWALKS-EVELYN-B083-WK1-PM1-CYBERSECURITY-LAB-SETUP

## Overview
This repository contains the step-by-step implementation, system configuration, and verification evidence for the **Cybersecurity Lab Setup** project. The lab environment is deployed on Oracle VM VirtualBox using Kali Linux on an isolated NAT network.

---

## 1. Environment Specifications
* **Host OS:** Windows 10
* **Hypervisor:** Oracle VM VirtualBox
* **Guest OS:** Kali Linux (`kali`)
* **Primary User:** `mwansa`
* **Admin User:** `labadmin`
* **Network Type:** VirtualBox NAT Network (`CyberLab`)
* **IP Subnet:** `10.0.0.0/24`
* **Static IP Assigned:** `10.0.0.2` (Gateway: `10.0.0.1`)

---

## 2. Implementation Steps

### Task 1: Network Configuration
1. Created a custom NAT Network named `CyberLab` with CIDR `10.0.0.0/24` in VirtualBox.
2. Configured Kali Linux interface (`eth0`) with static IPv4 address `10.0.0.2/24`.
3. Verified connectivity using `ping` tests to gateway (`10.0.0.1`) and DNS (`8.8.8.8`).

### Task 2: Service & Package Management
1. Updated local package repositories using `sudo apt update`.
2. Installed and enabled OpenSSH server (`openssh-server`).
3. Verified SSH daemon status via `systemctl status ssh`.

### Task 3: User & Key Authentication Setup
1. Created secondary administrative user `labadmin` and assigned to `sudo` group.
2. Generated ED25519 SSH key pair for passwordless/key-based authentication: `ssh-keygen -t ed25519 -C "labadmin@cyberlab"`.
3. Verified public key generation at `~/.ssh/id_ed25519.pub`.

---

## 3. Verification Screenshots

### Screenshot 1: Static IP Configuration
Verification of `10.0.0.2/24` assigned to `eth0`.
![Static IP Setup](./screenshots/screenshot1.png)

### Screenshot 2: Package Repository Update
Verification of completed `sudo apt update` execution.
![Package Update](./screenshots/screenshot2.png)

### Screenshot 3: OpenSSH Service Status
Verification of `openssh-server` running actively (`active (running)`).
![SSH Status](./screenshots/screenshot3.png)

### Screenshot 4: Public Key Generation
Verification of ED25519 public key output (`cat ~/.ssh/id_ed25519.pub`).
![SSH Public Key](./screenshots/screenshot4.png)

---

## 4. System Snapshots Log
* **Snapshot 1 (`Base Installation`):** Taken immediately after Kali OS installation and static IP (`10.0.0.2`) assignment.
* **Snapshot 2 (`Lab Complete`):** Taken after SSH activation, `labadmin` user creation, and ED25519 key generation.

---

## 5. Troubleshooting & Problem Resolution

### Issue Encountered
* **Problem:** Graphical display failure / black screen boot freeze during initial Kali Linux installation and post-installation system restart.

### Root Cause Analysis
* VirtualBox display adapter (`VMSVGA`) was conflicting with host-level Windows Hyper-V hypervisor services running in the background.

### Solution Applied
1. Disabled Hyper-V launch on the host via Windows Command Prompt (Admin):
   ```cmd
   bcdedit /set hypervisorlaunchtype off
