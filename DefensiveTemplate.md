# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology

The following machines were identified on the network:

<img src="https://github.com/edwardhough/wordpress-vuln/blob/main/images/image12.png" width=50% height=50%>

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

The target of this attack was: `Target Machine 1 - 192.168.1.110`

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers, as seen in the scan below:

<img src="https://github.com/edwardhough/wordpress-vuln/blob/main/images/image4.png" width=50% height=50%>

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### HTTP Request Size Monitor
Alert 1 is implemented as follows:
  - **Metric**: HTTP request size
  - **Alert rule**: WHEN sum() of http.request.bytes OVER all documents IS ABOVE 3500 FOR THE LAST 1 minute
  - **Threshold**: Above 3500 bytes for the last 1 minute
  - **Vulnerability Mitigated**: HTTP request smuggling, denial of service condition through high CPU usage
  - **Reliability**: TODO: Does this alert generate lots of false positives/false negatives? Reliability rating - Medium

#### CPU Usage Monitor
Alert 2 is implemented as follows:
  - **Metric**: CPU usage
  - **Alert rule**: WHEN max() OF system.process.cpu.total.pct OVER all documents IS ABOVE 0.5 FOR THE LAST 5 minutes
  - **Threshold**: Above 0.5 for the last 5 minutes
  - **Vulnerability Mitigated**: Malware performing malicious actions can cause spikes in CPU activity
  - **Reliability**: Does this alert generate lots of false positives/false negatives? Potentially. Reliability rating - Medium

#### Excessive HTTP Errors
Alert 3 is implemented as follows:
  - **Metric**: HTTP errors
  - **Alert rule**: WHEN count() GROUPED OVER top 5 'http.response.status_code' IS ABOVE 400 FOR THE LAST 5 minutes
  - **Threshold**: Above 400 errors for the last 5 minutes
  - **Vulnerability Mitigated**: Directory brute forcing
  - **Reliability**: Does this alert generate lots of false positives/false negatives? No. Reliability rating - High
