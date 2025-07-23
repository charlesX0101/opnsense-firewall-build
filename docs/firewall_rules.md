##OPNsense Firewall Rules and Access Policies

WAN
- Block all unsolicited inbound traffic by default
- No port forwarding rules configured at this time
- No services exposed to WAN
- Future VPN access will be handled by a separate rule set

LAN
- Allow full access to all internal networks (LAN, LAB, HOME, IOT, GUEST)
- Allow unrestricted access to the internet
- Intended for management, backup, monitoring, and administration
- Suricata IDS enabled in legacy mode on this interface

LAB
- Allow access to the internet
- Allow access to LAN for logging and monitoring
- Block all access to HOME, IOT, and GUEST
- Logging enabled for deny rules
- IDS enabled for research, testing, and detection purposes

HOME
- Allow access to the internet
- Allow access to IOT devices (for media casting and shared services)
- Block access to LAN, LAB, and GUEST
- Limited trust level, reserved for family and WFH devices

IOT
- Allow access to the internet
- Block all access to LAN, LAB, HOME, and GUEST
- No lateral communication permitted
- Used for smart TVs, cameras, printers, and untrusted devices

GUEST
- Allow access to the internet only
- Block all access to LAN, LAB, HOME, and IOT
- Completely isolated from internal traffic
- Intended for temporary visitor devices

Implementation Notes
- Each interface has an explicit allow rule for internet access
- Block rules are grouped using aliases or multi-destination selections
- All deny rules have logging enabled
- Rules are written to follow a top-down hierarchy from allow to deny
- Suricata IDS is active on LAN and LAB only
- No inbound NAT or port forwards are active as of this configuration

Future Rules
- WireGuard or OpenVPN access from WAN to LAB or LAN will be added
- Scheduled rules for LAB or GUEST isolation may be implemented
- IDS integration with monitoring system planned for alert visibility
