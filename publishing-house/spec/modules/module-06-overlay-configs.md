# Module 6: Overlay Configs

### Brief Overview

This module deploys the VXLAN EVPN overlay, completing the full fabric stack. Participants configure VTEPs, VNI mappings, VRF tenant design, anycast gateways, symmetric IRB, EVPN route targets and distinguishers, and PIM multicast replication across both Arista EOS and Cisco NX-OS platforms. The module concludes with end-to-end host connectivity validation across L2 stretch, intra-vendor inter-VLAN, and cross-platform inter-VLAN scenarios.

### Audience and Time

- **Target personas:** Network engineers implementing EVPN VXLAN overlays in multi-vendor data center environments
- **Prerequisites for this module:** Completion of Module 5 (underlay OSPF and eBGP routing operational)
- **Estimated duration:** 30 minutes

### Learning Objectives

- Deploy a VXLAN EVPN overlay including VTEPs, VNI mappings, VRF tenants, and anycast gateways across multi-vendor leaf switches
- Configure BGP EVPN address families, route targets, route distinguishers, and PIM multicast for VXLAN BUM traffic
- Verify end-to-end host connectivity across L2 stretch, intra-vendor inter-VLAN, and cross-platform inter-VLAN scenarios

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Review overlay design: VTEPs, VRFs, VNIs, anycast gateways | 8 min |
| 2 | Deploy the overlay configuration workflow | 10 min |
| 3 | Configure Linux hosts for connectivity testing | 5 min |
| 4 | Validate end-to-end host connectivity across the fabric | 7 min |

### Detailed Steps

1. Review the overlay design details: device roles (spine vs. leaf), VTEP configuration, VRF tenant "Tenant-A", VLAN-to-VNI mappings, route targets, route distinguishers
2. Understand symmetric IRB and anycast gateway configuration across leaf switches
3. Review VXLAN encapsulation, BGP EVPN address family configuration, and PIM sparse-mode for BUM traffic replication
4. Note the platform differences between Arista EOS and Cisco NX-OS for overlay features (nv overlay, feature vn-segment-vlan-based, etc.)
5. Launch the overlay configuration deployment workflow from AAP
6. Monitor the deployment and review the configuration applied to each device
7. Configure Linux container hosts with IP addresses and routes using docker exec commands (ip link set, ip addr add, ip route add)
8. Test L2 stretch connectivity: ping between hosts on the same VLAN across different leaf switches
9. Test intra-vendor inter-VLAN connectivity: ping between hosts on different VLANs behind the same vendor leaf pair
10. Test cross-platform inter-VLAN connectivity: ping between hosts behind Arista EOS leafs and hosts behind Cisco NX-OS leafs
11. Verify EVPN route tables on spine and leaf devices to confirm MAC/IP learning and route distribution

### Key Takeaways

- VXLAN EVPN provides L2 extension and L3 routing across the fabric with symmetric IRB for inter-VLAN traffic
- Anycast gateways enable distributed first-hop routing with the same virtual IP on every leaf
- Route targets and route distinguishers control EVPN route distribution across the multi-tenant fabric
- PIM sparse-mode handles BUM (Broadcast, Unknown unicast, Multicast) traffic replication in VXLAN
- Multi-vendor EVPN fabrics require careful attention to platform-specific feature enablement and configuration syntax
- End-to-end connectivity validation across L2, intra-vendor L3, and cross-platform L3 confirms complete fabric operation

### Infrastructure Notes

- The overlay depends on both base (Module 4) and underlay (Module 5) configurations being operational
- Linux hosts are Docker containers within Containerlab that require manual IP configuration for testing
- 4 Linux hosts are used for connectivity validation across the fabric
