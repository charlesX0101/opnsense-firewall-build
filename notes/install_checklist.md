##OPNsense Firewall Install Checklist

- Protectli Vault FW6E unboxed and inspected

- RAM installed into SODIMM slot

- SSD installed into internal bay

- Bottom case reassembled and verified

- OPNsense installer image downloaded

- Bootable USB created using official image

- USB inserted into Protectli unit

- System booted into installer via HDMI or serial

- OPNsense installed to internal SSD

- System rebooted and installer media removed

- Console used to assign WAN and LAN interfaces

- LAN IP confirmed and connected to switch

- OPNsense GUI accessed via web browser

- Default admin credentials updated

- Hostname set to fw-zero1

- Domain set to thebox.lan

- VLAN interfaces created for LAB, HOME, IOT, and GUEST

- Subnets assigned to each VLAN

- DHCP servers enabled for all internal interfaces

- Static IP reservations created for known hosts

- Firewall rules written per interface

- Explicit allow rules created for internet access

- Block rules applied to prevent lateral movement

- LAN granted full internal access

- LAB allowed access to internet and LAN logging only

- HOME allowed to access internet and IOT devices

- GUEST and IOT allowed internet only

- Logging enabled on all deny rules

- Suricata IDS enabled on LAN and LAB

- Verified routing and segmentation between all VLANs

- Confirmed DNS and DHCP function per zone

- Backed up firewall configuration to local file

- Next steps include configuring managed switch with VLAN tagging

- Mapping SSIDs to VLANs on Ubiquiti access point

- Deploying dedicated monitoring system in LAB subnet

