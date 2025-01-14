https://tryhackme.com/r/room/idsfundamentals
- Security that detects the activities of the connection that has passed through a firewall
- If an attacker has been able to bypass the firewall, the IDS can detect something that could be malicious happening within the network
- IDSs sit inside the network
- Upon every detection, an alert is sent to the Security Team(s)
	- The IDS will not act on those detections, only inform the relevant bodies that an alert has been created, and will give details around whatever activity it has picked up
- Again, the IDS does not prevent the threat after it detects it

Deployment Modes
- HIDS - Host Intrusion Detection System
	- Installed individually on hosts and cater for the detection of potential security threats associated with that single host only
	- Provide detailed visibility of the host's activities
	- Resource-intensive and require management on each host
		- Not scalable for large enterprises, not suitable*
- NIDS - Network Intrusion Detection System
	- Detects potentially malicious activities within the whole network
		- Regardless of any specific host
	- Monitors network traffic of all the hosts involved to detect suspicious activities
	- Provides a centralised view of all the detections inside the whole network

Detection Modes
- Signature-Based IDS
	- Each attack will have its own unique pattern, known as its signature
	- These signatures are kept in the DBs that the IDS use
		- So if the same attack happens again later, it will get detected by its signature and reported to the Security Team(s)
		- The stronger the signature database, the more efficiently it will detect known threats
		- Zero-day attacks, however, won't come up - as they are unique and freshly found exploits
			- They don't have any known signature just as yet
- Anomaly-Based IDS
	- Learns the baseline (normal behaviour) of the network or system and performs detections if there is any deviation from the normal pattern/behaviour of the system. 
	- Anomaly-based IDSs can detect zero-day exploits, as they don't rely on known signatures but a pattern of the systems behaviour
		- Comparing normal state to the current state (vice versa)
	- Can generate a lot of false positives, because most legitimate programs match the malicious ones
	- The Anomaly-based IDS can be fine-tuned (defining the baseline of the system)
- Hybrid IDS
	- Combines methods of both the Signature-based and Anomaly-based IDSs
- Signature-based IDSs can detect threats quickly, where the other IDSs can have a high processing overhead
- Signature-based IDSs can be good to cover a small threat surface
- The others, being able to pick up zero-day attacks/threats can be a useful option for larger organisations. 

Snort is an example of an IDS (Hybrid IDS)
- Modes
	- Packet Sniffer Mode
		- Reads and displays packets without doing any analysis on them
		- Not really an IDS capability, but good for network monitoring, troubleshooting etc
	- Packet Logging Mode
		- Detects network traffic in real-time and will display detections as alerts on the console for the Security Team to action
		- Allows the network traffic to be logged as a pcap file
		- Digital Forensic teams can use these log files to perform root cause analysis of attacks that may have been made
	- NIDS Mode
		- Primary mode that monitors the network and its traffic
		- Applies its rule files to identify any match to the known attack patterns stored in its signature database
		- If match happens, an alert is created
- You can run Snort on the host network or on the host and customise its rules (`/etc/snort/rules/local.rules`)
- You can also run Snort against a `.pcap` file to see if it can pick up any alerts from logs