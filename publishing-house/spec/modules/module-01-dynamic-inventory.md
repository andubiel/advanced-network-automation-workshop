# Module 1: Dynamic Inventory and Basic Setup

### Brief Overview

This module introduces the lab environment and guides participants through setting up dynamic inventory with Netbox as a Source of Truth. Participants connect to the lab via VS Code, examine inventory-as-code using ansible.controller modules, explore the AAP GUI inventory, create Netbox API tokens, configure Netbox as a dynamic inventory source, and validate multi-vendor device connectivity by gathering facts from Cisco NX-OS and Arista EOS network devices.

### Audience and Time

- **Target personas:** Network engineers and automation engineers with basic Ansible and networking knowledge
- **Prerequisites for this module:** Familiarity with Ansible inventory concepts, basic AAP Controller navigation
- **Estimated duration:** 30 minutes

### Learning Objectives

- Configure a Netbox API token and credential in Ansible Automation Platform
- Implement dynamic inventory using the netbox.netbox.nb_inventory plugin as a replacement for static inventory
- Verify multi-vendor network device connectivity by gathering facts from Cisco NX-OS and Arista EOS devices

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Connect to the lab environment via VS Code | 3 min |
| 2 | Open the AAP terminal in VS Code | 2 min |
| 3 | Examine inventory as code using ansible.controller modules | 3 min |
| 4 | Explore inventory in the AAP GUI | 3 min |
| 5 | Explore Netbox and understand device data | 3 min |
| 6 | Create a Netbox API token | 2 min |
| 7 | Update the Netbox credential in AAP | 2 min |
| 8 | Configure Netbox as inventory source with Ansible | 3 min |
| 9 | Validate the Netbox inventory configuration | 2 min |
| 10 | Sync dynamic inventory from Netbox | 3 min |
| 11 | Launch a job template to gather facts from network devices | 3 min |
| 12 | Troubleshooting (optional) | 1 min |

### Detailed Steps

1. Navigate to the VS Code tab in Showroom and connect to the lab environment
2. Open an integrated terminal in VS Code for AAP CLI access
3. Review the inventory-as-code playbook that uses ansible.controller.inventory, ansible.controller.group, and ansible.controller.host modules to define inventory programmatically
4. Navigate to the AAP Controller GUI and explore the pre-configured inventory structure (groups, hosts, variables)
5. Open the Netbox web interface and browse the device inventory, interfaces, and IP addressing data
6. Create a new API token in Netbox for Ansible integration
7. Update the Netbox credential in AAP Controller with the new API token
8. Review and run the playbook that configures the netbox.netbox.nb_inventory plugin as an inventory source in AAP
9. Validate the inventory source configuration by checking the AAP GUI
10. Trigger an inventory sync to pull device data from Netbox into AAP
11. Launch a job template that runs against the dynamic inventory to gather facts from all network devices, confirming multi-vendor connectivity
12. If issues arise, use containerlab inspect and containerlab redeploy commands to troubleshoot the lab topology

### Key Takeaways

- Netbox serves as a Source of Truth for network device inventory, replacing static inventory files
- The netbox.netbox.nb_inventory plugin enables dynamic inventory that stays current with infrastructure changes
- Ansible Controller modules (ansible.controller.*) allow inventory management as code
- Multi-vendor device fact gathering validates end-to-end connectivity between AAP and network devices

### Infrastructure Notes

- Containerlab must be running with all 6 network devices (2 spines, 4 leafs) accessible via SSH
- Netbox must be pre-populated with device records, interfaces, and IP addresses
- AAP Controller must have pre-configured credentials for network device access
