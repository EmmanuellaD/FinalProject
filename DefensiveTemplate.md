# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology


The following machines were identified on the network:
###Target 1
Operating System: Linux
Purpose: Target PC
IP Address: 192.168.1.110

###Target 2
Operating System: Linux
Purpose: Target PC
IP Address: 192.168.1.115


### Description of Targets

The target of this attack was: `Target 1` 192.168.1.110

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:


Alert 1:
Sum of HTTP Requests in Bytes is implemented as follows:

- **Metric: Sum of http.request.bytes over all documents
- **Threshold: above 3500 for the last minute 
- **Vulnerability Mitigated: port scans
- **Reliability: medium


Alert 2 is implemented as follows:
Count of HTTP response codes is implemented as follows:

- **Metric: When count count grouped over top 5 is http_response_status_code
- **Threshold: Above 400 for last 5 mins
- **Vulnerability Mitigated: failed attempts to access files/folders
- **Reliability: High

Alert 3 is implemented as follows:
CPU system process use is implemented as follows:
- **Metric: when max of system.process.cpu.total.pct over all documents
- **Threshold: Above .5 for last 5 mins
- **Vulnerability Mitigated: use of target as a slave or miner
- **Reliability: Medium


### Suggestions for Going Further (Optional) 
- Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain _how_ to implement each patch.

The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:
- Vulnerability 1- Excessive HTTP Errors
  - **Patch**:wordpress hardening
  - **Why It Works**: Implementing regular updates in wordpress as well as regular php version update and plugins would prevent vulnerable versions. Additionally, disabling unused features and removing specific paths would help make the site more secure

- Vulnerability 2- HTTP Request Size Monitor
  - **Patch**: Code Injection prevention
  - **Why It Works**: Implement an HTTP request limit on the web server as well as a input validation on all forms. It will help to prevent too large inputs and protect against malicious data  anyone attempts to send to the server via the website or application via HTTP request.

- Vulnerability 3- CPU Usage Monitor
  - **Patch**: Virus and malware hardening
  - **Why It Works**: Add update and good parameters to antivirus and use a Intrusion prevention system. The antivirus will detect, remove and prevent malicious activity while the IPS would both stop and monitor any unwanted activity
