# Module 4: Base Configurations

### Brief Overview

This module deploys foundational EVPN VXLAN base configuration across the multi-vendor spine-leaf fabric using a Backup-Deploy-Test workflow pattern. Participants configure hostnames, VLANs, loopback interfaces, physical interfaces, and IP addressing on both Arista EOS and Cisco NX-OS devices using resource modules. The module includes a role dispatch pattern for multi-vendor support, an intentional broken configuration troubleshooting exercise, and automated restore from backup.

### Audience and Time

- **Target personas:** Network engineers building multi-vendor data center fabrics with automation
- **Prerequisites for this module:** Completion of Modules 1-3 (inventory, backup, and compliance workflows operational)
- **Estimated duration:** 30 minutes

### Learning Objectives

- Deploy base fabric configuration (hostnames, VLANs, interfaces, IP addressing) across multi-vendor devices using Ansible resource modules
- Analyze the role dispatch pattern that routes platform-specific tasks to vendor-appropriate roles
- Troubleshoot an intentional broken fabric configuration and restore using the backup workflow

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Review the base configuration overview and role dispatch pattern | 5 min |
| 2 | Examine the Backup-Deploy-Test workflow structure | 3 min |
| 3 | Launch the base configuration deployment workflow | 5 min |
| 4 | Verify base configuration on network devices via SSH | 5 min |
| 5 | Deploy an intentionally broken configuration and troubleshoot | 7 min |
| 6 | Restore configuration from backup using the restore workflow | 5 min |

### Detailed Steps

1. Review the base_fabric role structure: understand how the dispatch pattern routes tasks to platform-specific roles (arista vs cisco) based on ansible_network_os
2. Examine the resource modules used: cisco.nxos.nxos_vlans, cisco.nxos.nxos_hostname, cisco.nxos.nxos_interfaces, cisco.nxos.nxos_l2_interfaces, cisco.nxos.nxos_l3_interfaces, and their arista.eos equivalents
3. Review the Backup-Deploy-Test workflow: backup current state, deploy new configuration, run connectivity tests
4. Launch the base configuration workflow from AAP and monitor execution
5. Review resource module output for each device, noting the commands applied and before/after state
6. SSH to spine1 (`ssh spine1`, then `enable`, `show run | b Ethernet`) to verify base configuration is applied
7. Launch the "broken fabric" playbook that introduces intentional misconfigurations
8. Run the connectivity test playbook to identify which devices or interfaces have issues
9. Analyze the test output to determine the nature of the broken configuration
10. Launch the restore workflow to recover the fabric to the previously backed-up good state
11. Re-run connectivity tests to verify the restore was successful

### Key Takeaways

- The role dispatch pattern enables a single playbook to manage multi-vendor environments by routing to platform-specific roles
- Resource modules provide consistent interface, VLAN, and IP configuration across Arista EOS and Cisco NX-OS
- The Backup-Deploy-Test workflow pattern ensures safe configuration changes with automatic rollback capability
- Automated connectivity testing validates fabric health after configuration changes
- Git-backed backups enable rapid restore when configuration issues are detected

### Infrastructure Notes

- All 6 network devices must be accessible and in a clean state before base configuration deployment
- The connectivity test playbook validates L3 reachability between devices
