https://tryhackme.com/room/splunk101

- Three main components:
	- Splunk Forwarder
		- An agent installed on the endpoint intended to be monitored
		- Main task is to collect data and send it to the Splunk instance
		- Does not affect the endpoints performance as its resource utilisation can be considered low
		- Some key data sources could be:
			- Web server generating web traffic
			- Windows machine generating Event Logs, PowerShell, Sysmon data
			- Linux host generating host-centric logs
			- Database generating DB connection requests, responses and errors
	- Splunk Indexer
		- Plays the main role in processing the data it receives from forwarders
			- Takes the data, 
			- normalizes it into field-value pairs
			- Determines the datatype of the data
			- Stores them as events
		- Processed data is easy to search and analyze
	- Search Head
		- The place within the Search & Reporting App where users can search the indexed logs
		- When the user searches for a term or uses a search language known as Splunk Search Processing Language - the request is sent to the indexer and the relevant events are returned in the form of field-value pairs
		- Search Head also provides the ability to transform the results into presentable tables, visualizations like pie-chart, bar-chart and column-chart

Data
- Splunk can ingest any data
- When data is added to Splunk, the data is processed and transformed into a series of individual events
- Data sources can be event logs, website logs, firewall logs, etc
- Data sources are grouped into categories
	- Files and directories
	- Network events
	- IT Operations
	- Cloud services
	- Database services
	- Security services
	- Virtualization services
	- Application servers
	- Windows sources
	- Other sources

- Incident Response Lifecycle
	- Preparation
		- Covers the readiness of an organisation against an attack
		- Documenting the requirements, defining the policies, incorporating the security controls to monitor like EDR/SIEM/IDS/IPS and so on
		- Staff training as well
	- Detection and Analysis
		- Everything related to detecting an incident and teh analysis process of the incident
		- Covers getting alerts from the security controls like SIEM/EDR investigating the alert to find the root cause
		- Also covers hunting for the unkown threat within the organisation
	- Containment Eradication and Recovery
		- Covers the actions needed to prevent the incident from spreading and securing the network
		- Involves steps taken to avoid an attack from spreading into the network, isolating the infected host, clearing th network from the infection traces, and gaining control back from the attack
	- Post Incident Activities
		- Includes identifying the loopholes in the organisation's security posture, which led to an intrusion, and improving so that the attack does not happen next time
		- The steps involve identifying weaknesses that led to the attack
		- Adding detection rules so that similar breaches do not happen again
		- Training staff.

- Cyber Kill Chain
	- Reconnaissance
		- An attempt to discover and collect information about a target
	- Weaponization
		- Malware can be created to avoid detection, and so on
		- Establish domains similar to the target domain to trick users
		- Create a C2 (Command and Control) server for the post-exploitation communication/activity and so on
	- Delivery
	- Exploitation
		- Attackers would need to exploit any found vulnerabilities (or selected ones) to gain access to systems
	- Installation
		- After a successful exploit, an attacker may attempt to install a backdoor or an application that will gain persistence or to gain further control of the system. 
	- Command and Control
	- Actions on Objectives

- Some good log sources
	- wineventlog
	- winRegistry
	- XmlWinEventLog
	- fortigate_utm
		- Fortigate firewall logs
	- iis
	- Nessus:scan
		- Results from the Nessus vulnerability scanner
	- Suricata
		- details of alerts from the Suricata IDS
		- shows which alert was triggered and what caused the alert to get triggered
	- stream:http
	- stream:DNS
	- stream:icmp

- Some Splunk commands: 
	```
	index="botsv1" "imreallynotbatman.com" sourcetype="stream*" 
	|  stats count(src_ip) as Requests by src_ip 
	|  sort -Requests
	```
	- Good way to get a count of requests made by src_ip
		- of all different network streams (dhcp, dns, http, icmp, ip, ldap, mapi, sip)
	- `index="botsv1" sourcetype=stream:http dest_ip="192.168.250.70"`
		- Will outline all inbound traffic to the given destination ip in the query
	```
	index="botsv1" sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST uri="/joomla/administrator/index.php" 
	|  table_time uri src_ip dest_ip form_data
	```
	- Good way to be able to get timed events of form_data requests made to a web-server
	- Summarises the type of form-data that was at play as well (for example, user logins to an admin console for Joomla - like the example above)
	```
		index="botsv1" sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST uri="/joomla/administrator/index.php" form_data=*username*passwd* 
	|  table_time uri src_ip dest_ip form_data
	```
	- Slightly changed but only including form_data contents that include 'username' and 'password'
	- Splunk has a function called **rex** for Regular Expressions.
		- `rex`
			- Specifies a Perl regular expression named groups to extract fields while you search
			- Example:
				- `... | rex field=_raw "From: (?<from>.*) To: (?<to>.*)"`
		- Extracting passwords following the earlier two examples above
			```
			index="botsv1" sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST uri="/joomla/administrator/index.php" form_data=*username*passwd* 
			|  rex field=form_data "passwd=(?<creds>\w+)" 
			|  table src_ip creds
			```
		- Have a look at the http_user_agent after doing an analysis similar to the one above - see what tends to hit. 
		- If there was a brute force attack (which would be obvious with the timestamps given in the http requests made) - you'd be able to find out more information around what kind of user-agent may have been involved
		```
			index="botsv1" sourcetype=stream:http dest_ip="192.168.250.70" http_method=POST uri="/joomla/administrator/index.php" form_data=*username*passwd* 
		|  rex field=form_data "passwd=(?<creds>\w+)"
		|  table _time src_ip uri http_user_agent creds
		```
		- Further to above, we can now specify more columns to display in the table
	- `index="botsv1" 192.168.250.70 ".exe" sourcetype="stream:http"`
		- Look out for any possible .exe files under the http data/tcp stream
		- Recall that you can further fine tune selected fields by looking at "`see all`" - you may find a field like `part_filename{}`
		- 