# Module 7: Tuning for Scale

### Brief Overview

This module demonstrates Ansible execution controls for scaling network automation safely. Participants use survey-driven job templates to configure SNMP across network devices while experimenting with serial batching, forks, throttle, and max_fail_percentage parameters. The module includes intentional error injection to illustrate canary deployment patterns and blast radius control at different failure tolerance settings.

### Audience and Time

- **Target personas:** Network automation engineers responsible for deploying changes safely across large device fleets
- **Prerequisites for this module:** Completion of Modules 1-6 (full fabric deployed and operational)
- **Estimated duration:** 25 minutes

### Learning Objectives

- Configure Ansible execution controls (serial, forks, throttle, max_fail_percentage) to manage deployment blast radius in network automation
- Implement survey-driven job templates for parameterized network configuration deployment
- Analyze the impact of different serial batch sizes and failure thresholds on canary deployment behavior

### Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Create a survey-driven job template for SNMP configuration | 5 min |
| 2 | Launch the job template with no errors to observe normal execution | 5 min |
| 3 | Launch with intentional errors to observe failure handling | 8 min |
| 4 | Compare different serial batch sizes and failure thresholds | 7 min |

### Detailed Steps

1. Review the configure_snmp.yml playbook and its use of execution control parameters
2. Create a survey-driven job template in AAP that allows specifying SNMP parameters at launch time
3. Launch the job template with correct parameters and observe successful execution across all network devices
4. Note the execution order and parallelism based on forks settings
5. Launch the job template with intentionally incorrect parameters to trigger failures on specific devices
6. Observe how serial batching controls which devices are affected: with serial: 1, only one device fails before the play stops
7. Re-run with larger serial batches (e.g., serial: 3) and observe how more devices are affected before failure detection
8. Experiment with max_fail_percentage to set a failure threshold -- e.g., 25% allows the play to continue as long as fewer than 25% of devices in the batch fail
9. Review throttle behavior for controlling concurrency on shared resources
10. Compare the blast radius across different combinations of serial, forks, and max_fail_percentage

### Key Takeaways

- Serial batching implements canary deployment patterns: deploy to a small batch first, then proceed to larger groups
- max_fail_percentage sets a failure tolerance threshold -- the play continues as long as failures stay below the threshold
- Forks controls parallelism within a batch, while throttle limits concurrency for shared resources
- Survey-driven job templates enable parameterized, self-service network configuration changes
- Combining these controls enables safe, scaled deployment strategies appropriate for production network environments

### Infrastructure Notes

- SNMP configuration is applied to all 6 network devices in the Containerlab topology
- Intentional error injection uses invalid SNMP parameters to trigger predictable failures
