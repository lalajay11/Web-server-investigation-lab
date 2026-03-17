# Web-server-investigation-lab
This investigation analyzed suspicious HTTP traffic targeting a Linux-based Apache web server. The server received multiple unauthorized requests probing sensitive path
Executive Summary
This investigation analyzed suspicious HTTP traffic targeting a Linux-based Apache web server. The server received multiple unauthorized requests probing sensitive paths such as /admin, /login, and /config. Packet captures and Apache access logs confirmed automated reconnaissance behavior originating from a single external IP address. No successful access to restricted areas occurred.
This activity is consistent with early‑stage scanning or enumeration performed by attackers before launching a targeted intrusion.
Environment Overview
• 	Operating System: Ubuntu Linux (VirtualBox VM)
• 	Web Server: Apache HTTP Server
• 	Network Interface: enp0s3
• 	Tools Used:
• 	Apache access logs
• 	tcpdump
• 	Wireshark (optional)
• 	Linux command-line utilities (grep, awk ,sort )
Suspicious Activity Overview
 Indicators of Reconnaissance
• 	Multiple HTTP GET requests to sensitive or administrative paths
• 	Requests occurred in rapid succession
• 	No valid authentication attempts
• 	No legitimate browser user-agent strings observed
Targeted Paths
The attacker probed:
• 	/admin
• 	/login
• 	/config
These paths are commonly targeted during reconnaissance to identify misconfigurations or exposed admin panels.
Attacker IP
• 	192.168.1.150 (example internal attacker IP used during simulation)
Evidence Collected
Apache Access Log Excerpts
GET /admin HTTP/1.1
GET /login HTTP/1.1
GET /config HTTP/1.1
Packet Capture
captured using: sudo tcpdump -1 enp0s3 -w suspicious_traffic.pcap
The .pcap file contains:
• 	Repeated HTTP GET requests
• 	No POST requests
• 	No authentication attempts
• 	No successful responses to restricted paths
Attack Pattern Analysis
Attack Type:
Automated reconnaissance/ directory enumeration
Behavior observed
• 	Rapid probing of common admin endpoints
• 	No session cookies or login attempts
• 	No browser-like behavior
• 	Consistent timing between requests (automation)
Risk Level:
Medium — reconnaissance is often the first stage of a larger attack.
Potential Attacker Goals:
• 	Identify exposed admin panels
• 	Detect misconfigured login pages
• 	Map server structure
• 	Prepare for brute-force or exploitation attempts
 Conclusion
The Apache access logs and packet capture confirm that the web server was targeted by automated reconnaissance activity. The attacker probed multiple sensitive paths in an attempt to discover administrative interfaces or misconfigurations. No successful access occurred, but the behavior represents a precursor to more aggressive attacks such as brute-force attempts or exploitation of known vulnerabilities.
Recommendations
• 	Restrict access to sensitive paths using authentication
• 	Implement rate limiting or request throttling
• 	Enable a Web Application Firewall (WAF)
• 	Monitor for repeated requests from the same IP
• 	Block attacker IP if appropriate
• 	Disable directory listing
• 	Keep Apache and system packages updated
Skills Demonstrated
• 	Web server deployment and configuration
• 	Apache log analysis
• 	Packet capture and inspection
• 	Reconnaissance detection
• 	SOC-style incident reporting
• 	Linux command-line investigation
• 	Evidence correlation
