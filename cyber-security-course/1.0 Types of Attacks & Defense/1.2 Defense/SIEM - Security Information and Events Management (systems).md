https://tryhackme.com/r/room/introtosiem
- 
- Host-Centric Log Sources
	- Log sources that capture events that occurred within or related to the host
	- ie
		- Windows Events logs
		- Sysmon
		- Osquery
		- and others
	- A user accessing a file
	- A user attempting to authenticate
	- A process Execution Activity
	- A process adding/editing/deleting a registry key or value
	- Powershell execution

- Network-Centric Log Sources
	- Generated when hosts communicate with each other or access the Internet to visit a website
	- SSH connections
	- A file being accessed via FTP
	- Web Traffic
	- A user accessing company's resources through VPN
	- Network file sharing activities

- SIEM Capabilities
	- Main Features
		- Threat detection
		- Investigation
		- Time to respond
	- Additional Features
		- Basic security monitoring
		- Advanced threat protection
		- Forensics & incident response
		- Log collection
		- Normalisation
		- Notifications and alerts
		- Security incident detection
		- Threat response workflow

- Devices generate hundreds of events per second (can)
- SIEMs only take logs from various sources in real-time but provide the ability to correlate between events, search through the logs, investigate incidents and respond in a timely manner
- Some key features of a SIEM:
	- Real-time log ingestion
	- Alerting against abnormal activities
	- 24/7 monitoring and visibility
	- Protection against the latest threats through early detection
	- Data insights and visualisation
	- Ability to investigate past incidents

- Every device on a network/system will generate a log activity whenever some kind of action is performed on it
- Windows Machine
	- Event Viewer
	- Logs from all Windows endpoints are forwarded to the SIEM for monitoring and better visibility 
- Linux Machines
	- Logs from Linux endpoints are also ingested into the SIEM for continuous monitoring
	- Common Linux log stores:
		- /var/log/httpd
			- Related to web-server (like Apache) HTTP requests/response and error logs
		- /var/log/cron 
			- Related to cron jobs (scheduled tasks)
		- /var/log/auth.log and /var/log/secure
			- Stores authentication related logs
		- /var/log/kern
			- Stores kernel related events

Log Ingestion
- Each SIEM will have their own method/way of ingesting logs 
	- Agent/Forwarder
		- These solutions are lightweight that get installed on the endpoint.
		- Configured to capture all the important logs and send them to the SIEM server
	- Syslog
		- Widely used protocol to collect data from various systems like web-servers, databased and so on
		- Are sent in real-time to the centralised destination
	- Manual Upload
		- These tools allow 'users' to ingest offline data for quick analysis 
		- Once the data is ingested, it is normalised and made available for analysis
	- Port-forwarding
		- SIEM solutions can also be configured to listen on a certain port
		- Endpoints forward the data to the SIEM instance on the listening port

SIEM Capabilities
- SIEMS collect logs, examine them, and if any event/flow has matched a condition set in rules or crossed a certain threshold - they will raise an alert for the SOC or Security Team to investigate and action accordingly
- Some capabilities:
	- Correlation between events from different log sources
	- Provide visibility on both Host-centric and Network-centric activities (in one interface/place)
	- Allow analysts to investigate the latest threats and timely responses
	- Hunt for threats that are not detected by the rules in place

SOC Analyst Responsibilities
- Monitoring and investigating
- Identifying false positives
- Tuning rules which are causing noise or false positives
- Reporting and compliance
- Identifying blind spots in the network visibility and covering them

Analysing Logs and Alerts
- Dashboard
	- Can bring together graphical representations of different kinds of traffic/system-usage etc
		- Outbound traffic by Country/Region (in Bytes, or whatever)
		- Inbound traffic by Country/Region (in Bytes or whatever)
		- Top Applications (Total Bytes or whatever)
		- DSCP - Precedence
			- Differentiated Services Code Point
				- A means of classifying and managing network traffic and of providing QoS in L3 IP networks
				- Uses 6-bit Differentiated Services (DS) field in the IP header for the purpose of packet classification
		- Top Services Denied through Firewalls (log source)
		- System Notifications
		- etc
- Correlation Rules
	- Logical expressions set to be triggered
	- Analysts can configure these to their requirements
		- If a user gets 5 failed login attempts in 10 seconds for example
		- If a login is successful after multiple failed login attempts
		- A rule is set to alert every time a user plugs a USB into their machine
		- If outbound traffic is > 50MB
		- etc etc
	- In-example:
		- Attackers/imposters tend to want to remove or clear the logs after they have carried out their evil-deeds
			- Event ID 104s can be reported every time a user tries to remove or clear event logs
			- "If the Log Source is WinEventLog AND EventID is 104 - TRIGGER AN ALERT `Event Log Cleared`"
		- Or say for example if a User tries to run a certain command, like `whoami` shortly after logging into a session
- Alert Investigation
	- Alert is a false positive - tuning the associated rules may be required in moving forward
	- Alert is a true positive - further investigate, contain etc
	- Contact the asset owner to inquire about the activity
	- Suspicious activity is confirmed, isolate the infected device(s)
	- Block the suspicious IP
	- etc
- 