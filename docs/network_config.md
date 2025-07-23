##Network Configuration Overview

This document outlines the VLAN and interface layout for the OPNsense firewall on the Protectli Vault FW6E. The design ensures strict separation between trust zones. It gives each zone its own subnet and DHCP scope.

Zone: LAN
Interface: lan
VLAN Tag: None
Subnet: 10.0.1.0/24
Firewall IP: 10.0.1.1
Purpose: Core management, backups, and admin systems

Zone: LAB
Interface: lab
VLAN Tag: 20
Subnet: 10.0.20.0/24
Firewall IP: 10.0.20.1
Purpose: Penetration testing boxes, security VMs

Zone: HOME
Interface: home
VLAN Tag: 30
Subnet: 10.0.30.0/24
Firewall IP: 10.0.30.1
Purpose: Trusted family and work-from-home devices

Zone: GUEST
Interface: guest
VLAN Tag: 40
Subnet: 10.0.40.0/24
Firewall IP: 10.0.40.1
Purpose: Visitor devices, isolated internet access only

Zone: IOT
Interface: iot
VLAN Tag: 50
Subnet: 10.0.50.0/24
Firewall IP: 10.0.50.1
Purpose: Smart devices, printers, cameras, untrusted hardware

Zone: WAN
Interface: wan
VLAN Tag: None
Subnet: DHCP from ISP
Purpose: Internet uplink via ARRIS S34 modem

DHCP Configuration
Each zone has a DHCP server enabled
Ranges are defined per subnet
Static IP reservations are created for known devices such as lab boxes, monitoring nodes, and admin systems

VLAN Trunking Notes
All VLANs are trunked to a TP-Link TL-SG2210MP managed switch
Switch ports will be assigned as access or trunk as needed
Ubiquiti U6+ access point will broadcast multiple SSIDs tagged to specific VLANs (HOME, GUEST, LAB)

Management Access
LAN is the only zone with access to the OPNsense web GUI
LAB is permitted to forward logs to LAN
All other zones are blocked from accessing management services

Routing and Isolation
Each subnet is isolated at Layer 3 by default
Firewall enforces routing restrictions between interfaces
No inter-zone communication occurs unless explicitly allowed in the firewall rule set
