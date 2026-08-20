# Module 5: Underlay Configs

### Brief Overview

This module deploys the OSPF routing and eBGP peering across the multi-vendor spine-leaf fabric using a hybrid approach of resource modules and Jinja2 templates. Participants explore when to use resource modules (for simple structured configuration) versus templates (where more control is needed), deploy underlay routing, and validate OSPF neighbor adjacencies, BGP peering, and IP reachability across the fabric.

### Audience and Time

- **Target personas:** Network engineers deploying routing underlay for EVPN VXLAN fabrics
- **Prerequisites for this module:** Completion of Module 4 (base fabric configuration deployed and validated)
- **Estimated duration:** 30 minutes

### Learning Objectives

- Deploy OSPF and eBGP underlay routing across a multi-vendor spine-leaf fabric using Ansible resource modules and Jinja2 templates
- Analyze the tradeoffs between resource modules and Jinja2 templates for network configuration management
- Verify underlay routing health using show commands for OSPF neighbors, BGP summaries, and routing tables

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Review resource modules vs. templates decision framework | 8 min |
| 2 | Deploy the underlay configuration workflow | 10 min |
| 3 | Validate underlay routing on network devices | 12 min |

### Detailed Steps

1. Review the pattern-by-deployment-stage approach: when resource modules are appropriate (simple, structured configuration like interfaces) versus when Jinja2 templates provide more control (complex routing protocol configuration)
2. Examine the OSPF and eBGP configuration templates and how they handle platform differences between Arista EOS and Cisco NX-OS
3. Review the EOS session-based configuration model and its implications for idempotency
4. Understand the idempotency tradeoffs when using templates (eos_config, nxos_config) compared to resource modules
5. Launch the underlay configuration workflow from AAP
6. Monitor the deployment output and note the rendered template configuration applied to each device
7. SSH to a network device and run `show ip ospf neighbor` to verify OSPF adjacencies are established
8. Run `show bgp evpn summary` (EOS) or `show bgp l2vpn evpn summary` (NX-OS) to verify BGP peering
9. Run `show ip route ospf` to verify OSPF-learned routes are present in the routing table
10. Run ping tests between loopback addresses to confirm end-to-end IP reachability across the underlay

### Key Takeaways

- Resource modules work best for simple, structured configuration (interfaces, VLANs); Jinja2 templates provide more control for complex protocols (OSPF, BGP)
- Template rendering translates data model variables into platform-specific CLI configuration
- The EOS session-based config model applies changes atomically, differing from NX-OS line-by-line application
- OSPF establishes the IP underlay while eBGP provides the EVPN control plane peering
- Comprehensive validation (OSPF neighbors, BGP peers, routing table, ping) confirms underlay health before overlay deployment

### Infrastructure Notes

- Base configuration from Module 4 must be successfully deployed before underlay routing can be established
- OSPF and BGP timers should be tuned for the Containerlab environment
