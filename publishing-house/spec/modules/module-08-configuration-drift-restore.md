# Module 8: Configuration Drift and Restore

### Brief Overview

This module teaches configuration drift detection and remediation using Git-stored intended state. Participants create named backup branches, introduce configuration drift (from the SNMP changes in Module 7), detect drift using the diff_against: intended parameter with config modules, and restore configurations to any named Git branch. This module ties together the backup, compliance, and restore workflows from earlier modules into a complete configuration lifecycle.

### Audience and Time

- **Target personas:** Network engineers responsible for configuration management, drift detection, and disaster recovery
- **Prerequisites for this module:** Completion of Modules 1-7 (full fabric deployed, SNMP changes from Module 7 introduce drift)
- **Estimated duration:** 25 minutes

### Learning Objectives

- Implement configuration drift detection using diff_against: intended with Git-stored configuration as the reference state
- Analyze drift detection output to identify specific configuration differences between running and intended state
- Automate configuration restore to any named Git branch using the ansible.scm and platform config modules

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Create a named backup branch capturing current (drifted) state | 5 min |
| 2 | Compare running configuration against the intended state branch | 7 min |
| 3 | Restore configuration to the initial backup branch | 6 min |
| 4 | Restore to the final (pre-drift) backup and validate | 7 min |

### Detailed Steps

1. Launch the backup workflow to create a new named branch capturing the current device configurations (which include SNMP drift from Module 7)
2. Review the backup branch in Gitea to see the stored configurations
3. Launch the drift comparison workflow that uses ansible.scm.git_retrieve to fetch the intended state branch and arista.eos.eos_config / cisco.nxos.nxos_config with diff_against: intended
4. Review the diff output to identify the SNMP configuration drift -- lines added by Module 7 that differ from the pre-Module-7 intended state
5. Interpret the diff format: lines prefixed with + are in running config but not in intended, lines prefixed with - are in intended but not in running
6. Launch the restore workflow targeting the initial backup branch (pre-SNMP, pre-Module-7 state)
7. Verify the restore by running the drift comparison again -- the diff should now be empty or minimal
8. Launch the restore workflow targeting the final backup branch (post-overlay, pre-drift state) as the production-ready configuration
9. Run a final validation to confirm the fabric is restored to the desired operational state
10. Review the congratulations section summarizing the complete workshop progression

### Key Takeaways

- diff_against: intended compares the running device configuration against a stored reference, enabling automated drift detection
- Git branches serve as named configuration snapshots, enabling point-in-time restore to any previous known-good state
- The ansible.scm collection integrates Git operations directly into Ansible workflows for configuration lifecycle management
- Drift detection and remediation close the loop on the configuration management lifecycle: backup, deploy, detect drift, restore
- Combining Source of Truth, backups as code, compliance, and drift detection provides a comprehensive network automation framework

### Infrastructure Notes

- SNMP configuration from Module 7 serves as the drift source -- Module 7 must be completed before this module
- Multiple Git branches must exist in Gitea for the restore comparison and selection workflow
