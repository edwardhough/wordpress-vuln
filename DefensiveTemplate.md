# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology

The following machines were identified on the network:
- Kali Machine
  - **Operating System**: Kali Linux
  - **Purpose**: Attacking
  - **IP Address**: 192.168.1.90
- ELK machine
  - **Operating System**: Ubuntu Linux
  - **Purpose**: Monitoring
  - **IP Address**: 192.168.1.100
- Target Machine 1
  - **Operating System**: Ubuntu Linux
  - **Purpose**: Vulnerable VM running WordPress
  - **IP Address**: 192.168.1.110
- Target Machine 2
  - **Operating System**: Ubuntu Linux
  - **Purpose**: Vulnerable VM running WordPress
  - **IP Address**: 192.168.1.105

### Description of Targets

The target of this attack was: **Target **Machine **1 - `192.168.1.110`

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### HTTP Request Size Monitor
Alert 1 is implemented as follows:
  - **Metric**: HTTP request size
  - **Alert rule**: WHEN sum() of http.request.bytes OVER all documents IS ABOVE 3500 FOR THE LAST 1 minute
  - **Threshold**: Above 3500 bytes for the last 1 minute
  - **Vulnerability Mitigated**: 
  - **Reliability**: TODO: Does this alert generate lots of false positives/false negatives? Rate as low, medium, or high reliability.

#### CPU Usage Monitor
Alert 2 is implemented as follows:
  - **Metric**: CPU usage
  - **Alert rule**: WHEN max() OF system.process.cpu.total.pct OVER all documents IS ABOVE 0.5 FOR THE LAST 5 minutes
  - **Threshold**: Above 0.5 for the last 5 minutes
  - **Vulnerability Mitigated**: TODO
  - **Reliability**: TODO: Does this alert generate lots of false positives/false negatives? Rate as low, medium, or high reliability.

#### Excessive HTTP Errors
Alert 3 is implemented as follows:
  - **Metric**: HTTP errors
  - **Alert rule**: WHEN count() GROUPED OVER top 5 'http.response.status_code' IS ABOVE 400 FOR THE LAST 5 minutes
  - **Threshold**: Above 400 errors for the last 5 minutes
  - **Vulnerability Mitigated**: TODO
  - **Reliability**: TODO: Does this alert generate lots of false positives/false negatives? Rate as low, medium, or high reliability.

The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:
- Vulnerability 1
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
- Vulnerability 2
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
- Vulnerability 3
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
