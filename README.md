# Infrastructure-as-Code (IaC) – Automated Network & Application Stack Provisioning

This project demonstrates a complete Infrastructure-as-Code implementation for provisioning a multi-VM network and deploying Docker-based services across Ubuntu Virtual Machines. The goal is to automate the creation, configuration, validation, and monitoring of a distributed application stack using VirtualBox, SSH automation, and containerized workloads.



1. Project Overview

The infrastructure consists of **three Ubuntu VMs**, each configured with:

- Static IP addresses
- SSH remote access
- Docker engine installation


IaC scripts (to be implemented) will automate VM provisioning, container deployment, and service health checks.


2. Key Features Implemented

### ✔️ 1. **VM Creation & Setup**
- Created **three Ubuntu 22.04 VMs** in VirtualBox.
- Allocated CPU, RAM, and storage as per requirement.
- Ensured NAT/Host-only adapter configuration for internal communication.

### ✔️ 2. **SSH Configuration**
- Enabled SSH on all VMs:
  ```bash
  sudo apt install openssh-server -y
  sudo systemctl enable ssh
  sudo systemctl start ssh
  
3. Docker Installation

Installed Docker Engine on all VMs:

sudo apt update
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker

4. Static IP Assignment (Netplan Configuration)

Set static IPs for all VMs under:

/etc/netplan/01-static.yaml

5. Challenges faced:
Netplan YAML Error Faced and Resolved

Initially, Netplan failed due to incorrect YAML:

nameservers:
  addresses: [8.8.8.8] im getting error over this


Problem: Extra text after the bracket made the YAML invalid.I faced a YAML formatting error in Netplan while configuring the nameserver section. 
The issue happened because I accidentally added extra text on the same line:
addresses: [8.8.8.8] im getting error over this

This caused Netplan to throw an “invalid YAML indentation/value” error during 
`sudo netplan apply`. I fixed it by correcting the YAML structure and removing 
the stray text. During troubleshooting I used chmod 600, chmod 644, and chmod 700 
to test and reset file permissions, finally setting the file to the correct 
permission (644).

Fix: Corrected indentation and removed stray text:

network:
  version: 2
  ethernets:
    ens33:
      dhcp4: no
      addresses:
        - 192.168.10.10/24
      gateway4: 192.168.10.1
      nameservers:
        addresses:
          - 8.8.8.8


Applied configuration:

sudo netplan apply




