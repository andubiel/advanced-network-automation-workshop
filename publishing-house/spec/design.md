# Advanced Ansible Network Automation Workshop

## Overview

This hands-on, intermediate-level lab extends the Introduction to Ansible Network Automation workshop into advanced network automation territory. Participants use Red Hat Ansible Automation Platform to deploy and validate a multi-vendor EVPN VXLAN switching fabric across Arista EOS and Cisco NX-OS devices running in Containerlab. The lab progresses through dynamic inventory setup with Netbox as a Source of Truth, Git-backed configuration backups using the ansible.scm collection, automated compliance enforcement with resource modules, full fabric deployment (base, underlay, overlay), execution tuning for safe scaled rollouts, and configuration drift detection with Git-based remediation. Throughout the workshop, participants interact with AAP Controller workflows, surveys, approval nodes, and multi-vendor resource modules.

## Target Audience

- **Role:** Network engineers, network automation engineers, infrastructure engineers
- **Experience level:** Intermediate (201-level, builds on introductory workshop)
- **What they already know:** Basic networking concepts (routing, switching, VLANs, VXLAN), Linux CLI proficiency, introductory Ansible and Ansible Automation Platform usage
- **What they don't know:** Source of Truth integration with dynamic inventory, multi-vendor resource module compliance patterns, EVPN VXLAN fabric deployment with Ansible, configuration drift detection and remediation at scale, AAP workflow orchestration with approval gates

## Prerequisites

- Basic networking knowledge: routing, switching, VLANs, VXLAN concepts
- Linux command-line proficiency
- Recommended: completion of the Introduction to Ansible Network Automation workshop
- Can the lab validate these automatically? Partially -- initial module validates connectivity to network devices and AAP environment

## Learning Objectives

1. Configure dynamic inventory using Netbox as a Source of Truth integrated with Red Hat Ansible Automation Platform
2. Automate multi-vendor network configuration backups to Git using the ansible.scm collection
3. Implement network compliance checks using resource modules with declarative state enforcement and AAP approval workflows
4. Deploy a multi-vendor EVPN VXLAN switching fabric across base, underlay, and overlay configuration layers
5. Configure Ansible execution controls (serial, forks, throttle, max_fail_percentage) for safe, scaled network deployments
6. Implement configuration drift detection and remediation using Git-stored intended state

## Content Type

Lab (hands-on)

## Products & Technologies

- Red Hat Ansible Automation Platform 2.6 (Controller, Execution Environments, Job Templates, Workflows, Surveys, Approval Nodes)
- Ansible Navigator
- Ansible Collections: ansible.controller, ansible.scm, ansible.netcommon, ansible.utils, arista.eos, cisco.nxos, netbox.netbox
- Arista EOS (vEOS 4.32.0F via Containerlab)
- Cisco NX-OS (Nexus 9000v 10.5.3.F via Containerlab)
- Containerlab
- Netbox
- Gitea
- VS Code (in-browser)
- Red Hat Enterprise Linux (bastion and control VMs)
- Networking technologies: EVPN VXLAN, OSPF, eBGP, PIM sparse-mode, SNMP, NTP, VRF, Anycast Gateway

## Module Map

| Module | Title | Duration |
|--------|-------|----------|
| 1 | Dynamic Inventory and Basic Setup | 30 min |
| 2 | Backups as Code | 25 min |
| 3 | Network Compliance | 30 min |
| 4 | Base Configurations | 30 min |
| 5 | Underlay Configs | 30 min |
| 6 | Overlay Configs | 30 min |
| 7 | Tuning for Scale | 25 min |
| 8 | Configuration Drift and Restore | 25 min |
| -- | **Total hands-on** | **~2 hours** |
| -- | Intro / overview pages | ~15 min |
| -- | **Total lab** | **~2 hours** |

## Difficulty Level

Intermediate

## Environment

**Learner view:** Two pre-provisioned RHEL VMs are available when the lab starts. The "containerlab" VM serves as a bastion host running Containerlab with 6 network devices (2 Arista EOS spines, 2 Arista EOS leafs, 2 Cisco NX-OS leafs) and 4 Linux container hosts forming a spine-leaf EVPN VXLAN topology. The "control" VM hosts Red Hat Ansible Automation Platform with pre-configured job templates, workflows, and credentials. Netbox is pre-populated with device inventory data. Gitea hosts Git repositories for configuration backups. VS Code is accessible in-browser for file browsing and editing. Showroom provides WeTTY terminal tabs for CLI access to both VMs and network devices.

**Automation needed:** Yes

Setup automation must provision: Containerlab topology with 6 network devices and 4 Linux hosts, Red Hat Ansible Automation Platform with pre-loaded job templates and workflows, Netbox with device and interface data, Gitea with backup repositories, VS Code server, and all required credentials and connectivity between components.

## Infrastructure Requirements

- **Cloud provider:** Troshka (nested virtualization required for Containerlab with Cisco n9kv and Arista vEOS)
- **Cluster type:** N/A (rhel-vms platform, no OCP cluster)
- **OCP version:** N/A (rhel-vms platform)
- **Topology:** Per-student
- **Sizing:** 2 VMs per student:
  - 1 containerlab VM (16 vCPU, 64GB RAM, 100GB disk) — Containerlab with 6 network devices + 4 Linux hosts, Netbox, Gitea, VS Code
  - 1 control VM (8 vCPU, 32GB RAM, 50GB disk) — AAP Controller
- **Automation approach:** Ansible (automation_type in spec)
- **AI/MaaS:** None
- **External services:** registry.gitlab.com (container images for network devices), gitlab.com (clones redhatautomation/201-multi-vendor-vxlan-workshop.git)
- **AAP version:** 2.6
- **Non-GA products:** None (all products are GA)

## Assessment Strategy (Optional)

Each module incorporates hands-on verification steps where participants validate their work through CLI show commands on network devices (e.g., show ip ospf neighbor, show bgp evpn summary), AAP job output inspection, and connectivity tests (ping between hosts across the fabric). Module 7 includes intentional error injection to verify participants can interpret failure behavior. The final module validates end-to-end drift detection and restore capabilities. Assessment is manual through observable outcomes rather than automated solve/validate buttons.
