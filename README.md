# OPNsense Firewall Segmentation for Homelab

## Overview

This repository documents the full build and setup of a segmented firewall using OPNsense on a Protectli Vault FW6E appliance. It is the main network part of a bigger homelab project focused on quality segmentation, monitoring, and security practices. The aim of this project is to create a strong firewall that isolates internal network zones, limits unnecessary traffic, and enforces least privilege access across the environment.

All hardware was set up from scratch, starting with unboxing and preparing the Protectli Vault. I manually installed the RAM and storage. Then, I flashed OPNsense onto a bootable USB and installed it on the unit. After OPNsense was installed, I brought the device online and configured it using the web GUI. I created logical interfaces and mapped them to VLANs, assigning each its own subnet and DHCP server. I added static IP reservations for known devices and defined gateway roles. Finally, I wrote firewall rules for each interface to control access between the network zones.

The Protectli device now acts as the main router and security appliance for the homelab network. It functions as the gateway, DHCP server, and firewall for five internal zones: LAN, LAB, HOME, IOT, and GUEST. It also has one WAN uplink connected to an ARRIS S34 cable modem.

## Network Zones

- LAN: Core management zone, admin systems, backups, SIEM access
- LAB: Penetration testing VMs, attack boxes, packet capture tools
- HOME: Trusted household and work-from-home devices
- GUEST: Visitor devices, isolated internet-only access
- IOT: Smart TVs, printers, cameras, and all untrusted hardware

Each zone has its own subnet and VLAN. OPNsense directly manages DHCP, and there are static reservations for key systems. Traffic between zones is blocked unless there is a specific rule that allows it.

## Features and Firewall Design

The firewall rules are set at the interface level and use a strict default-deny approach. Each zone includes a clear allow rule for internet access, followed by specific blocks against other internal zones. These blocks use grouped aliases and interface-based selections.

The LAN can access all zones and is reserved for trusted admin devices. The LAB can access the internet and send logs to the LAN zone, but it is blocked from accessing HOME, GUEST, and IOT. The HOME zone can reach the internet and interact with IOT devices for activities like casting, but it cannot access LAN, LAB, or GUEST. The IOT and GUEST zones are fully restricted from all internal communication and can access only the internet.

The rule design focuses on preventing lateral movement and ensuring a secure separation of trust zones. Logging is enabled on all deny rules for future review, and Suricata is deployed on the LAN and LAB interfaces in legacy mode for intrusion detection and anomaly logging.
## Future Work

This firewall project is part of a bigger homelab infrastructure build. Other components are in development and will be documented in separate repositories:

- A managed switch (TP-Link TL-SG2210MP) will be configured to trunk all VLANs to the appropriate ports. Ports will be assigned as access or tagged trunks based on host needs.
- A Ubiquiti U6+ access point will be added to broadcast multiple SSIDs tied to specific VLANs such as GUEST and HOME. This will allow wireless segmentation to match the wired structure.
- Another mini PC will be configured in the LAB zone to run a full monitoring stack including tools like Suricata, Zeek, syslog, and optionally an ELK stack. This system will serve as the logging and visibility hub for all network zones.
- A future project will introduce remote access via VPN, with strict firewall rules for ingress only from whitelisted clients.

Additional plans include using static route definitions for better internal segmentation, VLAN-aware services like local DNS, and alerting systems linked to network telemetry and firewall logs.

## Diagram

![Network Layout](images/general_layout.png)

## Images

The `/images/` folder contains a complete visual walkthrough of the project, including:
- Physical hardware preparation
- OPNsense installation steps
- Web GUI initialization
- Firewall rule layout
- Final dashboard views

## Docs

See the `/docs/` folder for full documentation on:

- Network and VLAN configuration
- Firewall rule breakdowns and access policies
- Step-by-step installation and setup process
- Detailed rationale for segmentation and rule design

This repository is meant to be both a personal guide and a high-quality example of practical network engineering, systems administration, and security design. It shows how open-source tools can be used to create a flexible and secure infrastructure in a real-world homelab environment.
