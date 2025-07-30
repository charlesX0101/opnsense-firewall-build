## OPNsense Firewall Rules and Access Policies

WAN
- Block all unsolicited inbound traffic by default
- No port forwarding rules configured at this time
- No services exposed to WAN
- Future VPN access will be handled by a separate rule set

LAN (VLAN 10)
- Allow full access to all internal VLANs: LAB, HOME, IOT, GUEST, and DMZ
- Allow unrestricted access to the internet
- Intended for admin tools, monitoring, troubleshooting, and backups
- Suricata IDS enabled in legacy mode on this interface
- Considered the trusted backbone of the homelab

LAB (VLAN 20)
- Allow access to the internet
- Allow access to LAN for logging, monitoring, and backup tasks
- Block all access to HOME, IOT, GUEST, and DMZ
- Logging enabled on deny rules
- IDS enabled for analysis, detection, and packet capture
- Used as primary management interface for firewall GUI

HOME (VLAN 30)
- Allow access to the internet
- Allow limited access to IOT devices (media casting, AirPlay, etc.)
- Block access to LAN, LAB, GUEST, and DMZ
- Moderate trust zone for family and work-from-home devices

IOT (VLAN 40)
- Allow access to the internet
- Block all access to LAN, LAB, HOME, GUEST, and DMZ
- No lateral communication permitted
- Fully isolated for security risk reduction
- Hosts include smart TVs, Ring cameras, consoles, and printers

GUEST (VLAN 50)
- Allow access to the internet only
- Block all access to LAN, LAB, HOME, IOT, and DMZ
- Completely isolated from internal traffic
- Used for visitors or any untrusted temporary devices

DMZ (VLAN 60)
- Block access to all other internal VLANs
- Allow outbound internet access only for testing purposes
- Intended for high-risk experimentation, honeypots, or external-facing labs
- Suricata not currently deployed here, but may be added in future

Implementation Notes
- All VLANs use interface-specific rules with a default-deny policy
- Internet access is granted via explicit allow rules per VLAN
- Block rules use grouped aliases or destination match groups
- Logging is enabled on all deny rules
- Rules are ordered top-down with permits before denies
- No inbound NAT or port forwards are active
- IDS/IPS is active on LAN and LAB interfaces only
- Firewall GUI is now served over VLAN 20 (LAB) for secure management

