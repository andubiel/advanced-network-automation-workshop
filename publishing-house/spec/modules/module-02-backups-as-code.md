# Module 2: Backups as Code

### Brief Overview

This module teaches participants to automate multi-vendor network configuration backups to Git using the ansible.scm collection. Participants run backup job templates in AAP, browse the resulting backup files in Gitea, and examine the playbook structure that uses git_retrieve and git_publish to manage configuration snapshots as versioned Git branches. The module also covers dynamically creating AAP job templates with survey menus populated from Git branches.

### Audience and Time

- **Target personas:** Network engineers and automation engineers responsible for configuration management and disaster recovery
- **Prerequisites for this module:** Completion of Module 1 (dynamic inventory configured and validated)
- **Estimated duration:** 25 minutes

### Learning Objectives

- Automate network configuration backups to Git branches using the ansible.scm git_retrieve and git_publish modules
- Analyze the multi-vendor backup playbook structure that handles both Arista EOS and Cisco NX-OS devices
- Create AAP job templates with survey menus dynamically populated from Git branch data using ansible.builtin.set_stats

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Run the backup job template to collect device configurations | 8 min |
| 2 | Locate and browse backup files in Gitea | 7 min |
| 3 | Examine the backup playbook structure and ansible.scm workflow | 10 min |

### Detailed Steps

1. Navigate to the AAP Controller GUI and locate the backup job template
2. Launch the backup job template and monitor its execution
3. Review the job output showing backup collection from each network device
4. Open Gitea and navigate to the backup repository
5. Use `git branch -r` or the Gitea UI to view the created backup branches
6. Browse the backup files to see device configurations stored per-host
7. Examine the backup playbook code: ansible.scm.git_retrieve clones the repo, arista.eos.eos_config and cisco.nxos.nxos_config collect backups, ansible.scm.git_publish commits and pushes
8. Review the use of ansible.builtin.set_stats to pass data between workflow nodes
9. Examine how downstream job templates use survey menus populated from Git branch names, enabling snapshot selection

### Key Takeaways

- The ansible.scm collection provides a Git-native workflow for storing network configurations as code
- git_retrieve and git_publish handle the clone-modify-commit-push cycle within Ansible playbooks
- Multi-vendor backups use platform-specific config modules (eos_config, nxos_config) with a shared Git workflow
- set_stats enables data passing between AAP workflow job nodes for dynamic survey population
- Named Git branches serve as configuration snapshots for later comparison and restore operations

### Infrastructure Notes

- Gitea must be pre-configured with a backup repository and appropriate credentials in AAP
- The backup workflow depends on network device connectivity established in Module 1
