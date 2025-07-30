##OPNsense Firewall Install and Setup Steps

This guide covers the complete installation process for the OPNsense firewall on a Protectli Vault FW6E. It documents the build from bare metal to a fully segmented firewall, including references to setup photos found in the /images/ folder.

#1. Unboxing and Preparation

The Protectli Vault FW6E was unboxed and inspected for physical condition. The device ships without RAM or storage pre-installed.

Image: ../images/01_unboxing.jpeg

#2. Installing RAM and Storage

The bottom panel was removed to access the internal slots. One stick of RAM and one SSD were installed. The case was reassembled and checked for seating.

Image: ../images/02_barebones.jpeg
Image: ../images/03_memory_storage_installed.jpeg

#3. Flashing OPNsense

OPNsense was flashed to a USB drive using the official installer image. The USB was connected to the Vault, which was booted into the installer via HDMI or serial console.

Image: ../images/04_starting_install.jpeg

#4. Installation Complete

After selecting the target disk and confirming the install, the firewall was rebooted into the OPNsense environment.

Image: ../images/05_install_complete.jpeg

#5. First Boot and Shell Access

On first boot, OPNsense shows the default console shell and prompts for interface assignments. The WAN and LAN interfaces were assigned manually at this stage.

Image: ../images/06_fresh_install.jpeg

#6. Interface Assignment and Configuration

Initial interface assignments were confirmed, and connectivity was tested. LAN was used to connect to the OPNsense web GUI.

Image: ../images/07_setting_up_io.jpeg

#7. Web GUI Access

Once LAN IP was configured, the OPNsense GUI was accessible via browser. The setup wizard was used to finish initial settings, including admin password, time zone, and hostname.

Image: ../images/08_welcome_screen_opnsense_gui.png

#8. VLANs and Logical Interfaces

VLANs were created for LAB, HOME, IOT, and GUEST. Each VLAN was assigned to a new interface and given its own subnet and DHCP configuration.

Configuration is documented in network_config.md.

#9. Firewall Rules and Segmentation

Firewall rules were written per interface to enforce isolation and limit lateral movement. Internet access was explicitly allowed per zone, and all other internal traffic was blocked except where exceptions were defined.

Rules are documented in firewall_rules.md
A visual overview is available in: ../images/firewall_rules.png

#10. Final Dashboard

The final result is a hardened, segmented OPNsense firewall appliance ready to route and secure all internal homelab traffic. The next steps include switch VLAN tagging, access point setup, and centralized monitoring.


