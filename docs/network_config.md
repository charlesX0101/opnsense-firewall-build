##Network Configuration Overview

This document outlines the finalized VLAN and interface layout for the OPNsense firewall running on a Protectli Vault FW6E. The configuration provides strong segmentation between zones, assigns a dedicated subnet and DHCP scope to each VLAN, and enforces strict Layer 3 isolation unless firewall rules explicitly allow communication.

Zone: LAN
Interface: LAN
VLAN Tag: 10
Subnet: 10.0.10.0/24
Firewall IP: 10.0.10.1
Purpose: Core administration, monitoring, and backup systems

Zone: LAB
Interface: LAB
VLAN Tag: 20
Subnet: 10.0.20.0/24
Firewall IP: 10.0.20.1
Purpose: Internal labs, penetration testing boxes, and the new primary management interface for accessing the OPNsense web GUI

Zone: HOME
Interface: HOME
VLAN Tag: 30
Subnet: 10.0.30.0/24
Firewall IP: 10.0.30.1
Purpose: Trusted household devices, work-from-home computers, and family phones

Zone: IOT
Interface: IOT
VLAN Tag: 40
Subnet: 10.0.40.0/24
Firewall IP: 10.0.40.1
Purpose: Untrusted hardware including Smart TVs, Ring cameras, printers, and consoles

Zone: GUEST
Interface: GUEST
VLAN Tag: 50
Subnet: 10.0.50.0/24
Firewall IP: 10.0.50.1
Purpose: Temporary visitor access, limited to internet-only connectivity

Zone: DMZ
Interface: DMZ
VLAN Tag: 60
Subnet: 10.0.60.0/24
Firewall IP: 10.0.60.1
Purpose: Air-gapped zone for honeypots, external-facing services, and high-risk experimentation

Zone: WAN
Interface: WAN
VLAN Tag: None
Subnet: DHCP from ISP
Purpose: Internet uplink via ARRIS S34 modem connected to igb0

DHCP Configuration

Each VLAN interface has a dedicated DHCP server enabled.
DHCP ranges are defined per subnet with reserved IPs for key systems.
Static reservations include workstations, monitoring nodes, media servers, and PXE boot utilities.
LAB and LAN both contain persistent infrastructure and logging devices.

VLAN Trunking and Switch Layout

igb1 is configured as the single trunk port connecting to a TP-Link TL-SG2210MP managed switch.
All VLANs (10–60) are tagged on trunk port 8.
Access ports on the switch are assigned per device requirements (access or tagged).
VLAN 20 (LAB) is also distributed through an unmanaged switch for lab workstations and experiments.
Ubiquiti U6+ access point is configured to broadcast SSIDs mapped to VLANs including HOME, GUEST, and LAB.

Management Access

LAB (VLAN 20) now hosts the OPNsense web GUI for firewall configuration.
LAN (VLAN 10) remains the fallback management zone for recovery and low-level access.
Other VLANs have no access to firewall services or internal management ports.

