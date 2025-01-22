https://tryhackme.com/r/room/snort

- Open-source, rule-based Network Intrusion Detection and Prevention System (NIDS/NIPS)
- Developed by Martin Roesch, open-source contributors and the Cisco Talos team.
- "*Snort is the foremost Open Source Intrusion Prevention System (IPS) in the world. Snort IPS uses a series of rules that help define malicious network activity and uses those rules to find packets that match against them and generate alerts for users*"

Intrusion Detection System (IDS)
- IDS is a passive monitoring solution for detecting possible malicious activities/patterns, abnormal incidents, and policy violations. 
- **It is responsible for generating alerts for each suspicious event.**
- There are two main types of Intrusion Detection Systems (IDSs):
	- Network Intrusion Detection System (NIDS)
		- Monitors the traffic flow from various areas of the network
		- The aim is to investigate the traffic on the entire subnet. 
		- If a signature is identified - **an alert is created**
	- Host-Based Intrusion Detection System (HIDS)
		- Monitors the traffic flow from a single endpoint device. 
		- The aim is to investigate the traffic on a particular device. 
		- If a signature is identified - **an alert is created**

Intrusion Prevention System (IPS)
- Intrusion Prevention Systems (IPSs) are an active protection solution for preventing possible malicious activities/patterns, abnormal incidents, and policy violations. 
- **It is responsible for stopping/preventing/terminating the suspicious event as soon as the detection is performed**
- There are four main types of IPS systems:
	- Network Intrusion Prevention System (NIPS)
		- Monitors the traffic flow from various areas of the network. The aim is to protect the traffic on the entire subnet.
		- If a signature is detected, **the connection is terminated**
	- Behaviour-based Intrusion Prevention System (Network Behaviour Analysis - NBA)
		- Behaviour-based systems monitor the traffic flow from various areas of the network. The aim is to protect the traffic on the entire subnet.
		- If a signature is identified, **the connection is terminated**
			- The difference between NIPS and Behaviour-based IPS's is that behaviour-based systems require a training period (also known as **baselining**) to learn the normal traffic and differentiate the malicious traffic and threats. This model provides more efficient results against new threats.
			- The system is trained to know the 'normal' to detect 'abnormal.' The training period is crucial to avoid any false positives. In case of any security breach during the training period, the results will be highly problematic. Another critical point is to ensure that the system is well trained to recognise benign activities. 
	- Wireless Intrusion Prevention System (WIPS)
		- Monitors the traffic flow from a wireless network. The aim is to protect the wireless traffic and stop possible attacks launched from there. 
		- If a signature is detected, **the connection is terminated**
	- Host-based Intrusion Prevention System (HIPS)
		- Actively protects the traffic flow from a single endpoint device. 
		- The aim is to investigate the traffic on a particular device. 
		- If a signature is identified, yep, you got it, **the connection is terminated.**
- HIPS and HIDS work with similar mechanisms - the main difference is that HIDS (Host-based Intrusion **Detection** System) will raise an alert when a signature is identified. 
	- HIPS on the other hand, it being a Intrusion **Prevention** System - will stop the attempt to stop the threat by termination its connection with the system (host in this case)

Detection/Prevention Techniques
- Signature-based
	- Relies on rules that identify the specific patterns of the known malicious behaviour. This model helps detect known threats
- Behaviour-based
	- Identifies new threats with new patterns that pass through signatures.
	- Compares the known/natural with unknown/abnormal behaviours. 
	- Helps detect previously unknown or new threats
- Policy-based
	- Compares detected activities with system configuration and security policies. 
	- Helps detect policy violations.

**TLDR**
- **IDS** identify threats, raise an alert - will require user or assistance to stop the potential threat
- **IPS** identifies the threat, raises an alert (at this point I am suspecting that it will raise an alert, because it should), and will block the threat by itself (with less user assistance at the detection time)

"*Snort can be deployed inline to stop these packets, as well. Snort has three primary uses: As a packet sniffer like tcpdump, as a packet logger - which is useful for network traffic debugging, or it can be used as a full-blown network intrusion prevention system. Snort can be downloaded and configured for personal and business use alike*"

Capabilities of SNORT:
- Live traffic analysis
- Attack and probe detection
- Packet logging
- Protocol analysis
- Real-time monitoring
- Modules & plugins
- Pre-processors
- Cross-platform support (Linux & Windows)

Three main-use models:
- Sniffer Mode
- Packet Logger Mode
- NIDS (Network Intrusion Detection System) and NIPS (Network Intrusion Prevention System)

Commands
- `snort -V`
	- Get the version of Snort and check if it is installed
- `snort -c /etc/snort/snort.conf -T`
	- Check the config to ensure it's valid
	- `-T` is for testing the configuration
	- `-c` is identifying the config file to test
	- Config file addresses:
		- Rules
		- Plugins
		- Detection mechanisms
		- Default actions
		- Output settings
		- and probably heaps more
	- You can have multiple config files for different purposes and cases **but can only use one at runtime**
- Sniffer Mode
	- `-v` 
		- Verbose
		- Display the TCP/IP output in the console
	- `-d`
		- Display the packet data (payload)
		- Covers verbose mode and provides more data
	- `-e`
		- Display the link-layer (TCP/IP/UDP/ICMP) headers
	- `-X`
		- Display the full packet details in HEX
	- `-i`
		- Helps to define a specific network interface to listen/sniff
		- Once you have multiple interfaces, you can choose a specific interface to sniff
- Logger Mode
	- You can use Snort as a sniffer and log the sniffed packets via logger mode
	- You only need to use the packet logger mode parameters, and snort does the rest to accomplish this
	- `-l`
		- **Logger mode**
		- Target log and alert output directory
			- Default output folder is `/var/log/snort`
		- The default action is to dump as tcpdump format in `/var/log/snort`
	- `-K ASCII`
		- Log packets in ASCII format
	- `-r`
		- Reading option, read the dumped logs in Snort
	- `-n`
		- Specify the number of packets that will process/read. 
		- Snort will stop after reading the specified number of packets 

- Logfile Ownership
	- Whoever creates a file becomes the owner of the corresponding file
		- Simple
	- Snort will need superuser rights to sniff traffic, so once snort is run with the `sudo` command, `root` account will own the related output files
	- Change the ownership of files/directories (to the respective user and/or group(s))
	- `sudo chown <username> <file>`
	- `sudo chown <username> -R <directory>` 
		- Recursive to all contents that are within said directory

- Snort in IDS/IPS mode
	- (N)IDS/IPS mode depends on the rules and configuration
	- `-c` 
		- Defining the configuration file
	- `-T`
		- Testing the configuration file
	- `-N`
		- Disable logging
	- `-D`
		- Background mode
	- `-A`
		- Alert modes
			- full
				- providing all possible information about the alert
					- Also the default mode (if you don't specify any mode, this one will be the one that Snort will default to)
			- fast
				- Shows the alert message, timestamp, source and destination IPs, along with port numbers
			- console
				- Fast style alerts on the console screen
			- cmg
				- CMG style, basic header details with payloads in hex and text format
				- Full packet details - real neat
			- none
				- Disable alerting..
			- Example
				- `sudo snort -c /etc/snort/snort.conf -N -A console`
					- Will disable logging
					- Will enable console alerts (pretty cool!)
					- Remember, these are based on predefined rules for the IDS to pick up :) 

- Using Rule File without Configuration File
	- Helps in testing user-created rules
	- This mode provides less performance
	- `sudo snort -c /etc/snort/rules/local.rules -A console`
		- Note that we aren't pointing `-c` to the `snort.config` file in this instance

- IPS Mode and Dropping Packets
	- `-Q --daq afpacket`
		- You can also activate this mode by editing the `snort.conf` file
		- `-Q` 
			- Enables inline mode operation
		- `--daq`
			- Select packet acquisition module (default is pcap)

Reading PCAP files
- You can have a pcap file and process it with Snort
- You will receive default traffic statistics with alerts depending on your ruleset
- Reading a pcap without using any additional parameters we discussed will only overview the packets and provide statistics about the file
	- Not very useful
- We're using Snort to investigate the pcap file to benefit from the rules it has and to help speed up our investigation process by using the known patterns of threats.
- PCAP mode parameters:
	- `-r / --pcap-single=` 
		- Read a single pcap file
		- `sudo snort -c /etc/conf/snort/conf -q -r test.pcap -A console`
	- `--pcap-list=""`
		- Read pcaps provided in command (**SPACE separated** `" "` )
		- `sudo snort -c /etc/snort/snort.conf -q --pcap-list="test1.pcap test2.pcap test3.pcap" -A console`
	- `--pcap-show`
		- Show pcap name on console during processing
		- `sudo snort -c /etc/snort/snort.conf -q --pcap-list="test1.pcap test2.pcap" -A console --pcap-show`
			- Will show the name of the .pcap file just before reading from it. So you know which file contains the given strings/alerts

SNORT Rule Structures
 ![](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/58234314551a2962ad5617cb22591a2b.png)
		(above image from THM snort lab/module)
- Rule contents:
		- Action
			- Alert
				- Generate an alert and log the packet
			- Log
				- Log the packet
			- Drop
				- Block and log the packet
			- Reject
				- Block the packet, log it, and terminate the packet session.
		- Protocol
			- TCP, UDP, ICMP, IP
			- NOTE:
				- Snort2 supports only the four protocol filters (as above) in the rules
				- HOWEVER, you can detect application layer protocols/flows by using port numbers and options
				- ie if you want to detect FTP traffic, you cannot use the FTP keyword in the protocol field, but, you can filter the FTP traffic by investigating TCP traffic on port 21 for example.
		- Source IP
			- ANY (but you can define other things I'd suspect)
			- IP ranges
				- `alert icmp 192.168.1.0/24 any <> any any (msg: "ICMP Packet Found"; sid: 100001; rev:1;)`
				- This rule will create an alert for each ICMP packet originating from the 192.168.1.0/24 subnet
			- Multiple IP ranges
				- `alert icmp [192.168.1.0/24,10.1.1.0/24] any <> ...`
				- Will sniff and alert on both subnets listed above
			- Exclude IP addresses/ranges
				- `alert icmp !192.168.1.0/24 any <> ...`
				- The exclamation point (`!`) negates/excludes specific addresses and ports
		- Source Port
			- ANY (as above)
				- `alert tcp any any <> any 21 ...`
				- This rule will create an alert for each TCP packet SENT to Port 21 (we want SFTP or FTPS right ;) ) 
			- Negating a port (same with the exclamation point `!` )
				- `alert tcp any any <> any !22 ...`
			- Filter a port-range
				- `alert tcp any any <> any 1:1024 ...`
					- Will alert for each TCP packet sent to ports between 1 and 1024
			- Filter a port-range type 2
				- `alert tcp any any <> any:1024 ...`
					- Will alert for each TCP packet sent to ports less than or equal to 1024
			- Filter a port-range type 3
				- `alert tcp any any <> any 1025 ...`
					- Alert for each TCP packet sent to a source port higher than or equal to 1025
			- Filter a port-range type 4
				- `alert tcp any any <> any [21,23] ...`
					- Alert for each TCP packet sent to port 21 and 23
		- Direction
			- <> 
			- Inbound, outbound I'm thinking
			- `>` 
				- Source to destination flow
			- `<>`
				- Bidirectional flow
			- NOTE:
				- there is no `<` in SNORT
		- Destination IP
			- ANY (but can be something else if you pick something up I'd imagine to make a custom rule towards a C2 server or something)
		- Destination Port
			- ANY
		- Options
			- Msg
			- Reference
			- Sid
			- Rev
	- Example
		- `alert icmp any any <> any any (msg: "ICMP Packet Found"; reference:CVE-XXXX; sid: 1000001; rev:1;)`
		- "alert" for IDS mode
		- "reject" for IPS mode
	- **Rules can not be processed without a header.**
	- Rule options are ***optional*** parts
		- It is almost impossible to detect sophisticated attacks without using the rule options

Three Main Rule Options in Snort
- General Rule Options
	- Fundamental rule options
- Payload Rule Options
	- Options that help to investigate the payload data
	- These options are helpful to detect specific payload patterns
- Non-payload Rule Options
	- Options that focus on non-payload data
	- Help create specific patterns and identify network issues

General Rule Options
- `Msg`
	- Message field is a basic prompt and quick identifier of the rule
	- Once the rule is triggered, the message filed will appear in the console and/or log
	- Usually the message part is a one-liner that summarises the event
- `Sid`
	- SNORT RULE ID (SID)
	- Come with a pre-defined scope
	- Each rule must have a SID in proper format, there are three different scopes for SIDs:
		- `<100` 
			- Reserved Rules
		- `100-999,999`
			- Rules came with the build
		- `>=1,000,000`
			- Rules created by user/teams
	- Rules we create should have a SID that is higher than 100,000,000. SID should never overlap and each id must be unique
- `Reference`
	- Each rule can have additional information or references to explain the purpose of the rule or threat pattern
	- That could be a CVE identifier, or external information
	- Having reference for the rules will always help analysts during the alert and incident investigation
- `Rev`
	- Snort rules can be modified and updated for performance and efficiency issues
	- `Rev` option helps analysts to have the revision information for each rule
	- It will be easy to understand rule improvements
	- Each rule has its unique Rev Number, and there is no auto-backup feature on the rule history
	- **Analysts should keep the rule history themselves**
	- `Rev` options is only an indicator of how many times the rule had revisions
			`alert icmp any any <> any any (msg: "ICMP Packet Found", sid: 100001; reference:cve,CVE-xxxx; rev:1;)`

Payload Detection Rule Options
- Content
	- Payload data. 
	- Matches specific payload data by ASCII, HEX, or both
	- Possible to use this option multiple times in a single rule
	- However, the more you create specific pattern match features, the more it takes time to investigate a packet.
	- Following rules will create an alert for each HTTP packet containing the keyword "GET". **This rule option is case sensitive**
		- ASCII mode
			- `...(msg: "GET Request Found"; content:"GET"; sid: 100001; rev:1;)`
		- HEX mode
			- `...(msg:GET Request Found"; content:"|47 45 54|";sid: 100001;rev1;)`
- Nocase
	- Disabling case sensitivity. Used for enhancing the content searches
	- `alert tcp any any <> any 80 (msg: "GET Request Found"; content:"GET"; nocase; sid:100001; rev:1;)`
- Fast_pattern
	- Prioritise content search to speed up the payload search operation
	- By default, Snort uses the biggest content and evaluates it against the rules
	- "fast_pattern" option helps you select the initial packet match with the specific value for further investigation
	- This option always works case insensitive and can be used once per rule. 
	- Note that this option is required when using multiple "content" options. 
	- The following rule has two content options, and the fast_pattern option tells Snort to use the first content option (in this case, "GET") for the initial packet amtch
		- `alert tcp any any<> any 80 (msg: "GET Request Found"; content:"GET"; fast_pattern; content: "www"; sid:100001;rev:1;)`

Non-Payload Detection Rule Options
- These options can help create specific patterns and identify network issues
	- `ID`
		- Filtering the IP id field
			- `alert tcp any any <> any any (msg:"ID TEST";id:123456;sid: 100001; rev:1;)`
		- The ID field in an IP Packet Header is used to identify a packet in a communication session
	- `Flags`
		- Filtering the TCP flags
			- `F` - FIN
			- `S` - SYN
			- `R` - RST
			- `P` - PSH
			- `A` - ACK
			- `U` - URG
		- `alert tcp any any <> any any (msg: "FLAG TEST";flags:S; sid: 100001; rev;1;)`
	- `Dsize`
		- Filtering the packet payload size
			- `dsize:min<>max;`
			- `dsize:>100`
			- `dsize:<100`
		- `alert ip any any <> any any (msg: SEQ TEST"; dsize100<>300; sid: 100001; rev:1;)
	- `Sameip`
		- Filtering the source and destination IP addresses for duplication.
			- `alert ip any any <> any any (msg: "SAME-IP TEST"; sameip; sid: 100001; rev:1;)`
- Remember that when you create rules, it will be a **local rule** and will have to be in your `local.rules` file
	- `sudo vim /etc/snort/rules/local.rules`
- NOTE: there are default rules that are activated with a Snort instance

Points to Remember:
- Main components of Snort
	- Packet Decoder
		- Packet collector component of Snort
		- It collects and prepares the packets for pre-processing
	- Pre-processors
		- A component that arranges and modifies the packets for the detection engine
	- Detection Engine
		- The primary component that processes, dissects and analyses the packets by applying related rules
	- Logging and Alerting
		- Log and alert generation component
	- Outputs and Plugins
		- Output integration modules (ie, alerts to syslog/mysql) and additional plugin (rule management detection plugins) support is done with this component

There are three types of rules available for Snort
https://www.snort.org/downloads
- Community Rules
	- Free ruleset under the GPLv2
	- Publicly accessible, no need for registration
- Registered Rules
	- Free ruleset (however, requires registration)
	- This ruleset contains subscriber rules with 30-days delay
- Subscriber Rules (Paid)
	- Paid ruleset
	- This ruleset is the main ruleset and is updated twice a week (Tuesdays and Thursdays)
You will need to ensure that each rule is outlined in the snort.conf file if you are considering using the community or paid rules

Editing the `snort.conf` File
- Snort has several rule updating modules and integration tools
- To sum up, never replace your configured Snort configuration files
	- **You MUST edit your configuration files manually or update your rules with additional tools and modules to not face any fail/crash or lack of feature(s)**
		- `snort.conf` 
			- Main configuration file
		- `local.rules`
			- User-generated rules file
- `sudo vim /etc/snort/snort.conf`
	- Step #1: "Set the network variables" section
		- HOME_NET
			- That is what we are protecting
				- `any` or `192.168.1.1/24`
		- EXTERNAL_NET
			- This field is the external network, so we need to keep it as `any` or `!$HOME_NET`
				- `any` or `!$HOME_NET`
		- RULE_PATH
			- Hardcoded rule path
				- `/etc/snort/rules`
		- SO_RULE_PATH
			- These rules come with registered and subscriber rules
				- `$RULE_PATH/so_rules`
		- PREPROC_RULE_PATH
			- These rules come with registered and subscriber rules
				- `$RULE_PATH/plugin_rules`
	- Step #2: "Configure the decoder." section
		- Manages the IPS mode of Snort
		- Single-node installation model IPS model works best with `afpacket` mode
		- You can enable this mode and run Snort in IPS
			- `#config daq:` 
				- IPS mode selection
					- `afpacket`
			- `#config daq_mode`
				- Activating the inline mode
					- `inline`
			- `#config logdir`
				- Hardcoded default log path
					- `/var/logs/snort`
			- Data Acquisition Modules (DAQ)
				- specific libraries used for packet I/O
				- Bringing flexibility to process packets
				- It is possible to select DAQ type and mode for different purposes
				- There are six DAQ modules available in Snort
					- `Pcap`
						- Default mode, known as Sniffer Mode
					- `Afpacket`
						- Inline mode, known as IPS Mode
					- `Ipq`
						- Inline mode on Linux by using Netfilter
						- It replaces the snort_inline patch
					- `Nfq`
						- Inline mode on Linux
					- `Ipfw`
						- Inline on OpenBSD and FreeBSD by using divert sockets, with the pf and ipfw firewalls
					- `Dump`
						- Testing mode of inline and normalisation
				- The most popular modes are the `pcap` and `Afpacket` modes
	- Step #6: "Configure Output Plugins" section
		- Manages the outputs of the IDS/IPS actions
			- Such as logging and alerting format details
		- The default action prompts everything in the console application, so configuring this part will help you use Snort more efficiently
	- Step #7: "Customise your Ruleset" section
		- `# site specific rules`
			- Hardcoded local and user-generated rules path
				- `include $RULE_PATH/local.rules`
		- `#include $RULE_PATH/`
			- Hardcoded default/downloaded rules path
				- `include $RULE_PATH/rulename`
		- NOTE that the `#` is a commenting operator
			- UNCOMMENT IT if you want to activate it :) 