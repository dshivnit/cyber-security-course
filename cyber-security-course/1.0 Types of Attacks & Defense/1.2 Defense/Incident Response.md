https://tryhackme.com/r/room/incidentresponsefundamentals

- Events through a system are normally stored in logs
- Some of these events could point towards something malicious happening on the system
- Issue is that there are **a lot** of events that occur, picking the ones that can be recognised as alerts can be tricky
- There are, however, security solutions that can be set in place that will be able to identify the harmful events and report them to the respective Security Teams
- Some of these alerts could be false positives, and some true
- Examples:
	- False Positive:
		- A security solution raised an alert on an event where there was a high amount of data being transferred from one system to an external IP address. 
		- Upon analysis, the Security Team found that the internal system was in the middle of a backup process to a cloud storage solution. 
	- True Positive:
		- A security solution raised an alert on a phishing attempt on one of the company's employees
		- Upon analysis, the Security Team found that the email was indeed a malicious email sent to the user to compromise the system
- True positives are regarded as incidents

- Incident Severity
	- Categorisations:
		- Low
		- Medium
		- High

Types of Incidents (some)
- Malware Infections
- Security Breaches
- Data Leaks
	- Unlike a security breach, data leaks could be due to unintentional actions/mistakes by humans or misconfigurations - human error
- Insider Attacks
	- An internal employee will always have greater access to the system than outsiders
	- They can essentially affect an entire system (like on their last day before saying, "ciao")
- Denial of Service Attacks

Incident Response Process
- SANS - SysAdmin, Audit, Network, and Security
	- SANS Response Framework - PICERL
		- Preparation
			- First phase
			- Building the necessary resources to handle an incident. 
			- Include developing a Security Response Team, having a proper Incident Response Plan in place, deploying necessary security solutions to combat the incidents
		- Identification
			- Refers to looking for any abnormal behaviour that may indicate an incident
			- Using various security solutions and techniques to monitor abnormal events
		- Containment
			- When an incident has been identified, contain it so that its impact will be minimised
			- Perhaps isolate a compromised machine, disable the compromised user account, and so on depending on the context
		- Eradication
			- Removing the threat from the attacked environment
			- Ensure that the subject environment is clean
		- Recovery
			- Recovering the affected systems from backup or rebuilding them
			- Then test the recovered systems and ensure that they are ready to use
		- Lessons Learned
			- Gaps in the detection and analysis of the incident are identified and documented
			- Helping to improve the overall process in future incidents
- NIST - National Institute of Standards and Technology
	- NIST Incident Response Framework (similar to SANS)
		- Preparation
		- Detection and Analysis
		- Containment, Eradication and Recovery (in one phase)
		- Post-Incident Activity

Key components of the Incident Response Plan:
- Roles and Responsibilities
- Incident Response Methodology
- Communication Plan (with stakeholders, including law enforcement)
- Escalation path to be followed

Some Security Solutions that can assist the Security Team(s):
- SIEMs (Security Incident and Event Management)
	- Collects important logs from various systems/devices and correlates them into one centralised location to be able to allow Security Teams' to identify incidents
- AV (Anti Virus)
	- Detects known malicious programs in a system and regularly scans the system(s) in place
- EDR (Endpoint Detection and Response)
	- Deployed on every system, protecting it against advanced-level threats
	- Can also contain and eradicate the threat

Playbooks
- Step-by-step instructions to deal with each kind of incident
- Can help save time
- **Guidelines** for a comprehensive incident response
- Example (Incident: Phishing Email):
	- Notify all stakeholders of the phishing email content
	- Determine if the email was malicious by conducting header and body analysis of the email
	- Look for any attachments within the email and analyse them
	- Determine if anybody had opened the email
	- Isolate the infected systems from the network
	- Block the email sender

Runbooks
- Detailed, step-by-step **execution** of specific steps during different incidents
- These steps will vary depending on the resources that are available for the investigation

