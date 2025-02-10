https://tryhackme.com/room/wazuhct
https://wazuh.com/

- Created in 2015

- An EDR (Endpoint Detection and Response) tool
	- EDRs are a series of tools and applications that monitor devices for an activity that could indicate a threat or a security breach, some features:
		- Auditing a device for common vulnerabilities
		- Monitoring a device for suspicious activities such as unauthorised logins, brute-force attacks or privilege escalations
		- Visualising complex data and events into neat and trendy graphs (lol)
		- Recording a device's normal operating behaviour to help with detecting anomalies (baselining)

- Operates on a management (manager) and agent module
	- Agents monitor the processes and events that take place on a device
		- (ie authentication and user management)
	- Agents will then offload these logs to a designated collector for processing, such as Wazuh

- Vulnerability Assessment Module
	- This tool can be used to periodically scan an agent's OS for installed applications and their version numbers
	- This information is then sent back to the Wazuh Server and compared against a database of CVEs to discover potential vulnerabilities
	- This tool will perform a full scan when the Wazuh Agent is first installed
		- it must be configured to run at a set interval after that first initial scan (by default, it is set to every five (5) minutes)
	- Out of the box, the rulesets that are configured (by default) to check for an agent system's compliance are quite sensitive. 

- Policy Auditing
	- After the Wazuh Agent is installed on an endpoint - an audit is performed where a metric is given using multiple frameworks and legislations such as NIST, MITRE, GDPR, TSC, HIPAA, PCI DSS

- Monitoring Logons and other events via rules
	- Wazuh > Management > Rules

- Collecting Windows Logs
	- Agent config file will need to be updated to reflect logs/events picked up from Sysmon on the device
	- Config file location:
		- `C:\Program Files (x86)\ossec-agent\ossec.conf`
		```
		<!-- Sysmon Analysis -->
		<localfile>
		<location>Microsoft-Windows-Sysmon/Operation</location>
		<log_format>eventchannel</log_format>
		</localfile>
		```
	- Restart the Agent, preferably the whole OS
	- The Wazuh Management Server will need to have Sysmon added as a rule to visualize these events 
	- This can be done by adding an XML file to the local rules located in:
		- `/var/ossec/etc/rules/local_rules.xml`
		```
		<group name="sysmon,">
			<rule id="255000" level="12">
			<if_group>sysmon_event1</if_group>
			<field name="sysmon.image">\\powershell.exe||\\.ps1||\\.ps2</field>
			<description>Sysmon - Event 1: Bad exe: $(sysmon.image)</description>
			<group>sysmon_event1,powershell_execution,</group>
			</rule>
		</group>
		```
	- The server too will have to be restarted afterwards for this change to the rules file to take effect

- Collecting Linux Logs
	- Rules are located in:
		- `/var/ossec/ruleset/rules`
	- Rulesets such as the `0250-apache_rules.xml` rules if wanting to be used would need to be inserted into the Wazuh Agent's config file - located in:
		- `/var/ossec/etc/ossec.conf`
- Auditing Commands on Linux
	- `auditd` package is utilised and installed on Wazuh agents running on Debian/Ubuntu and CentOS OSs
	- `auditd` monitors the system for certain actions and events and will write this to a log file
	- The log collector module on Wazuh's agent can be used to read the log file and send it to the Wazuh Management Server for processing
	- Audit rules are located in:
		- `/etc/audit/rules.d/audit.rules`

- Wazuh's API (to set up your own client)
	- https://documentation.wazuh.com/current/user-manual/api/reference.html
	- The API Console is quite interactive
		- Accessed via the Management Console
			- Wazuh > Tools > API Console

- Generating Reports
	- Modules > Security Events (for example) > adjust the date range you want to generate a report from > Generate Report (top-right hand side)
	- Once generated > Management > Reporting to view generated reports 

- Generating some sample data
	- Settings > Sample Data
	- Three different options
	- Pretty neat!
