https://tryhackme.com/r/room/zeekbro
https://docs.zeek.org/en/master/about.html

*My thinking towards the end of the first lab/module here - is to use Wireshark to gather as much network traffic as possible in any given scenario that will generate a .pcap file used for investigation*
*Then use Zeek to go through an analyse the check out of that .pcap file :)* 
*Teamwork, always, in this case, collaboration between tools (I'm still very nub)*

- Open-source and commercial network monitoring tool (network analyser)
- Developed by Lawrence Berkeley Labs
- A supplemental tool for investigations into malicious or suspicious activity
- Network monitoring is a daily part of IT/NOC operations and differs from Network Security Monitoring (NSM) in its purpose
- Network monitoring aims to detect and reduce network problems, improve performance and in some cases, increase overall productivity

Network Monitoring
- Highly focused on IT assets like uptime (availability), device health and connection quality (performance), and network traffic balance and management (configuration). 
- Monitoring and visualising the network traffic, troubleshooting, and root cause analysis are also part of the Network Monitoring process. 
- This model is helpful for network administrators and usually doesn't cover identifying non-asset in-depth vulnerabilities and significant security concerns like internal threats and zero-day vulnerabilities. 
- Usually, Network Monitoring is not within the SOC scope
	- It is linked to the enterprise IT/Network management team

Network Security Monitoring
- Focused on network anomalies like rogue hosts, encrypted traffic, suspicious service and port usage, and malicious/suspicious traffic patterns in an intrusion/anomaly detection and response approach
- Monitoring and visualising the network traffic and investigating suspicious events is a core part of Network Security Monitoring. 
- This model is helpful for security analysts/incident responders, security engineers and threat hunters and covers identifying threats, vulnerabilities and security issues with a set of rules, signatures and patterns.. 
- Network Security Monitoring is part of the SOC, and the actions are separated between tier 1-2-3 level analysts. 

ZEEK vs SNORT
- Capabilities:
	- Zeek:
		- NSM and IDS framework
		- Heavily focused on network analysis
		- Focused on specific threats to trigger allerts
		- The detection mechanism is focused on events
	- Snort:
		- An IDS/IPS system
		- Heavily focused on signatures to detect vulnerabilities 
		- Detection mechanism is focused on signature patterns and packets
- Cons
	- Zeek:
		- The analysis is done out of the Zeek, manually or by automation
	- Snort:
		- Hard to detect complex threats
- Pros:
	- Zeek:
		- It provides in-depth traffic visibility
		- Useful for threat hunting
		- Ability to detect complex threats
		- It has a scripting language and supports event correlation
		- Easy to read logs
	- Snort:
		- Easy to write rules
		- Cisco supported rules
		- Community support
- Common Use Case:
	- Zeek:
		- Network monitoring
		- In-depth traffic investigation
		- Intrusion detecting in chained events
	- Snort:
		- Intrusion detection and prevention
		- Stop known attacks/threats

Zeek Architecture
- Event Engine
	- Where the packers are processed
	- It is called the event core and is responsible for describing the event without focusing on event details
	- It is where packages are divided into parts such as source and destination addresses, protocol identification, session analysis and file extraction.
- Policy Script Interpreter
	- Where the semantic analysis is conducted
	- Responsible for describing the event correlations by using Zeek scripts

Zeek Frameworks
- Has several frameworks to provide extended functionality in the scripting layer
- These frameworks enhance Zeek's flexibility and compatibility with other network components
- Each framework focuses on the specific use case and easily runs with Zeek installation
- Available Frameworks:
- https://docs.zeek.org/en/master/frameworks/index.html
	- Logging
	- Cluster
	- Signature
	- Notice
	- Broker Communication
	- Summary
	- Input
	- Supervisor
	- NetControl
	- Configuration
	- GeoLocation
	- Packet Analysis
	- Intelligence
	- File Analysis
	- TLS Decryption

Zeek Outputs:
- Zeek provides 50+ log files under seven categories, which are helpful in various areas such as traffic monitoring, intrusion detection, threat hunting and web analytics. 
- Logs are held in 
	- `opt/zeek/logs`

Working with Zeek
- `zeekctl status`
- `zeekctl start`
	- `start`
- `zeekctl stop`
	- `stop`
- `status`
- The only way to listen to live network traffic when using Zeek is to use it as a service
- Apart from Zeek being a network monitoring tool, it can also be used as a packet investigator
	- To do so, we need to process a pcap file with it
	- `zeek -C -r sample-file.pcap`
	- Zeek will automatically create log files associated to the pcap file that it is processing in the working directory that the zeek command is run from
	- `r` - reading option, read/process a pcap file
	- `-C` - ignoring checksum errors
	- `-v` - version information
	- `zeekctl` - ZeekControl module
- Log investigation
	- Will require CLI tools like `cat`, `cut`, `grep`, and `uniq`
	- Zeek generates log files according to traffic data
	- You will have logs for every connection in the wire, including the application level protocols and fields
	- Zeek can identify 50+ logs and categorises them into seven categories
		- Well structured, tab-separated ASCII files
	- Logs Summary
		- Network
			- Network Protocol Logs
				- conn.log, dce_rpc.log, dhcp.log, dnp3.log, dns.log, ftp.log, http.log, irc.log, kerberos.log, modbus.log, modbus_register_change.log, mysql.log, ntlm.log, ntp.log, radius.log, rdp.log, rfb.log, sip.log, smb_cmd.og, smb_files.log, smb_mapping.log, smtp.log, snmp.log, socks.log, ssh.log, ssl.log, syslog.log, tunnel.log
		- Files
			- File analysis result logs
				- files.log, ocsp.log, pe.log, x509.log
		- NetControl
			- Network control and flow logs
				- netcontrol.log, netcontrol_drop.log, netcontrol_shunt.log, netcontrol_catch_release.log, openflow.log
		- Detection
			- Detection and possible indicator logs
				- intel.log, notice.log, notice_alarm.log, signatures.log, traceroute.log
		- Network Observations
			- Network flow logs
				- known_certs.log, known_hosts.log, known_modbus.log, known_services.log, software.log
		- Miscellaneous
			- Additional logs cover external alerts, inputs and failures
				- barnyard2.log, dpd.log, unified2.log, unknown_protocols.log, weird.log, weird_stats.log
		- Zeek Diagnostic
			- Zeek diagnostic logs cover system messages, actions and some statistics
				- broker.log, capture_loss.log, cluster.log, config.log, loaded_scripts.log, packet_filter.log, print.log, prof.log, reporter.log, stats.log, stderr.log, stdout.log
	- https://docs.zeek.org/en/current/script-reference/log-files.html
	- https://corelight.com/products/zeek-data/
- Some logs are updated daily, and some per session - as below:
	- Daily
		- known_hosts.log
			- List of hosts that completed TCP handshakes
		- known_services.log
			- List of services used by hosts
		- known_certs.log
			- List of SSL certificates
		- software.log
			- List of software used on the network
	- Per Session
		- notice.log
			- Anomalies detected by Zeek
		- intel.log
			- Traffic contains malicious patterns/indicators
		- signatures.log
			- List of triggered signatures
- Brief log usage primer table
	- Overall Info
		- conn.log
		- files.log
		- intel.log
		- loaded_scripts.log
	- Protocol Based
		- http.log
		- dns.log
		- ftp.log
		- ssh.log
	- Detection
		- notice.log
		- signatures.log
		- pe.log
		- traceroute.log
	- Observation
		- known_hosts.log
		- known_services.log
		- software.log
		- weird.log
- You can categorise logs before starting an investigation. 
- Finding the evidence/anomaly you are looking for will be easier
- Make sure you read each log description and understand the purpose to know what to expect from the related log file
- Don't just rely on the logs above!
- The above categorisation shows us how to use multiple logs to identify anomalies and run an investigation by correlating across the available logs
	- Overall Info
		- The aim is to review the overall connections, shared files, loaded scripts, and indicators at once
		- This is the first step of the investigation
	- Protocol Based
		- Once the overall traffic has been reviewed and suspicious indicators have been found, or we want to conduct a more in-depth investigation, we can focus on a specific protocol
	- Detection
		- Use the prebuilt or custom scripts and signature outcomes to support findings by having additional indicators or linked actions
	- Observation:
		- Summary of the hosts, services, software and unexpected activity statistics will help you discover possible missing points and conclude the investigation

Example of a conn.log
```
#separator \x09
#set_separator	,
#empty_field	(empty)
#unset_field	-
#path	conn
#open	2025-01-25-02-53-47

#fields	ts	uid	id.orig_h	id.orig_p	id.resp_h	id.resp_p	proto	serviceduration	orig_bytes	resp_bytes	conn_state	local_orig	local_resp	missed_bytes	history	orig_pkts	orig_ip_bytes	resp_pkts	resp_ip_bytes	tunnel_parents

#types	time	string	addr	port	addr	port	enum	string	interval	count	count	string	bool	bool	count	string	count	count	count	count	set[string]
```

Reading Logs
- Technical knowledge and event correlation ability will be needed. 
	- As logs provide a vast amount of data to investigate and correlate
- The use of external visualisation and correlation tools such as ELK and Splunk can be used (hoping to touch more on this later)
- One auxiliary program called `zeek-cut` reduces the effort of extracting specific columns from log files
- Each log file provides "field names" in the beginning, this information will help when using `zeek-cut`. 
- Make sure that you use the "fields" and **NOT** the "types"
	- `zeek-cut`
		- Cuts specific columns from zeek logs
		- `cat conn.log | zeek-cut uid proto id.orig_h id.orig_p id.resp_h id.resp_p`
			- Extracting only the uid, protocol, source and destination hosts and source and destination ports from the conn.log

Zeek Signatures
- Zeek supports signatures to have rules and event correlations to find noteworthy activities on the network
- These signatures use low-level pattern matching and cover conditions similar to Snort rules
- Unlike SNORT rules, Zeek rules are NOT the primary event detection point
	- Zeek has a scripting language and can chain multiple events to find an event of interest
	
- Zeek Signatures are composed of three logical path
	- Signature ID
		- Unique signature name (like the signature's primary key)
	- Conditions
		- Header
			- Filtering the packet headers for specific source and destination addresses, protocol and port numbers
		- Content
			- Filtering the packet payload for specific value/pattern
	- Action
		- Default action
			- Create the signatures.log file in case of a signature match
		- Additional action
			- Trigger a Zeek script

- Most common conditions and filters for Zeek Signatures
	- Header
		- src-ip
		- dst-ip
		- src-port
		- dst-port
		- ip-proto
	- Content
		- payload
		- http-request
		- http-request-header
		- http-request-body
		- http-reply-header
		- http-reply-body
		- ftp
	- Context
		- same-ip
			- Filtering the source and destination addresses for duplication
	- Action
		- event
			- Signature match message
	- Comparison Operators
		- == , != , < , <= , > , >=
	- NOTE
		- Filters accept string, numeric and regex values

- Running a signature
	- `zeek -C -r sample.pcap -s sample.sig`
		- `-s` - Use a signature file

- Sample Signature
	```
	signature http-password {
		ip-proto == tcp
		dst-port == 80
		payload /.*password.*/
		event "Cleartext Password Found!"
	}
	```
	- Zeek signatures support regex
		- Regex `.*` matches any character zero or more times
		- The rule will match when a password phrase is detected in the packet payload
		- Once the match occurs, Zeek will generate an alert and create additional log files (signatures.log and notice.log)
	```
	signature ftp-admin {
		ip-proto == tcp
		ftp /.*USER.*dmin.*/
		event "FTP Admin Login Attempt!"
	}
	```
	- This signature can be considered a case signature
	- While it is accurate and works fine, we need global signatures to detect the "known threats/anomalies." We will need those case-based signatures for significant and sophistical anomalies like zero-days and insider attacks in the real-life environment. 
	- Having individual rules for each case will create dozens of logs and alerts and cause missing the real anomaly
	- The critical point is logging logically, not logging everything

	- We can improve our signature by not limiting the focus only to an admin account. 
	- In that case, we need to know how the FTP protocol works and the default response codes. 
	- If you don't know these details - you can refer to this: 
		- https://datatracker.ietf.org/doc/html/rfc765
	- A revised version of the previous signature, one which will capture ALL failed FTP login attempts
	```
	signature ftp-brute {
		ip-proto == tcp
		payload /.*530.*Login.*incorrect.*/
		event "FTP Brute-force attempt"
	}
	```
	(I wouldn't really call it a brute-force, as it could have been just a general mistake a user had made when trying to login.)
	- A signature file can consist of multiple signatures
	- So we can have one file for each protocol/situation/threat type
		```
		signature ftp-admin{
			ip-proto == tcp
			ftp /.*USER.*dmin.*/
			event "FTP Admin Login Attempt!"
		}

		signature ftp-brute {
			ip-proto == tcp
			ftp /.*530.*Login.*incorrect.*/
			event "FTP Brute-force attempt"
		}
		```
		- Then when wanting to filter out what we need:
			- `cat notice.log | zeek-cut uid id.orig_h id.resp_h msg sub | sort -r | nl | uniq | sed -n '1001,1004p'

Zeek Scripts
Zeek scripts are based on their own programming language, similar to other high-level programming languages. It is a skill to learn how to use this language efficiently
- Base Scripts
	- **Do NOT modify these**
		- `/opt/zeek/share/zeek/base`
	- User-generated or modified scripts should be in their own path
		- `opt/zeek/share/zeek/site`
	- Policy scripts are located in
		- `/opt/zeek/share/zeek/policy`
	- To automatically load/use a script in live sniffing mode, the Zeek config file will need to be modified (you can also use a script for a single run, similar to signatures)
		- `/opt/zeek/share/zeek/site/local.zeek`
- Zeek scripts use the `.zeek` extension
- Calling scripts in live monitoring mode by loading them with the command
	- `load @/script/path`, or
	- `load @script-name`
- **Zeek is event-oriented, not packet-oriented!**
- Need to use/write scripts to handle the event of interest

- With Wireshark, you can pull information like DHCP hostnames from a pcap file (as with tcpdump, tshark or Zeek) 
	- However, it's not simple to transfer that data to another tool for processing
- With CLI based tools, it' easy to extract and transfer data to another tool for processing and correlating
	- **tcpdump** example:
		- `sudo tcpdump -ntr captureRequest.pcap port 67 or port 68 -e -vv | grep 'Hostname Option' | awk -F: '{print $2}' | sort -nr | uniq | nl`
	- **tshark** example:
		- `tshark -V -r captureRequest.pcap -Y "udp.port==67 or udp.port==68" -T fields -e dhcp.option.hostname | nl | awk NF`
	- Here's a Zeek example (script and command):
		- Script:
			```
			event dhcp_message (c: connection, is_orig: bool, msg: DHCP::Msg, options: DHCP::Options)
			{
			print options$host_name;
			}
			```
			- The only part that is created here is the third line which will tell Zeek to extract DHCP hostnames
			- The other lines are the predefined syntaxes of the scripting language
		- `zeek -C -r captureRequests.pcap dhcp-hostname.zeek`
		- No need for numerous piping
		- Making Zeek more efficient when wanting to extract data and for correlation
		- Zeeks own training platform (FREE!!)
			- https://try.bro.org/#/?example=hello
- There are multiple options to trigger conditions in Zeek
- There is a Built-in Function (BiF) and protocols to extract information from traffic data
- You can find supported protocols and BiF (Built-in Function) by looking at your own setup, or visiting the Zeek repo (https://try.bro.org/#/?example=hello)

Writing Basic Scripts
- Operators, types, attributes, declarations and statements, and directives
	- `event zeek_init() { print ("Started Zeek!"); }` and `event zeek_done() { print ("Stopped Zeek!"); }`
		- Do have proper spacing though please
	- And you'd be able to run it with `zeek -C -r sample.pcap basic.zeek`
		- `Started Zeek!\nStoppedZeek!`
- Another one:
	```zeek
	event new_connection(c: connection)
	{
		print c;
	}
	```
	- This will provide a bulk data set for each connection
	- Not the best usage, and realistically thinking we'd need to filter the information for specific purposes. There is an ID and field for each part
	```zeek
	event new_connection(c: connection)
	{
		print ("###########################");
		print ("");
		print ("New Connection Found!");
		prinit ("");
		print fmt ("Source Host: %s # %s --->", c$id$orig_h, c$id$orig_p);
		print fmt ("Destination Host: resp: %s # %s <---", c$id$resp_h, c$id$resp_p);
		print ("");
	}
	```
	- `%s` - Identifies string output for the source
	- `c$id` - Source reference field for the identifier
	- This would filter the event(s) of interest
	- Using the primary tag (which in this case is `c` - which comes from `c: connection` 
	- The script above creates logs and prompts each source and destination address for each connection

Using Scripts and Signatures Together
- One step closer to event correlation!
- Zeek scripts can refer to Zeek signatures as well as with other Zeek scripts
	- Provides a big advantage for correlation :) 
- Example of the **script**:
	```zeek
	event signature_match(state: signature_state, msg: string, data: string)
	{
		if (state$sig_id == "ftp-admin")
		{
			print ("Signature hit! --> #FTP-Admin ");
		}
	}
	```
- Example of the **ftp-admin signature**:
	```zeek
	signature ftp-admin
	{
		ip-proto == tcp
		ftp /.*USER.*admin.*/
		event "FTP Username Input Found!"
	}
	```
	- `zeek -C -r sample.pcap -s ftp-admin.sig 201.zeek`
	- This script will quickly check if there is a signature hit and provides terminal output to notify us
	- We are using "signature_match" event to accomplish this
	- We are looking only for **"ftp-admin"** signature hits
	- Events
		- https://docs.zeek.org/en/master/scripts/base/bif/event.bif.zeek.html

Loading Local Scripts
- `/opt/zeek/share/zeek/base`
- One can load all the local scripts identified in your `local.zeek` file
- Note that base scripts cover multiple framework functionalities
- You can do this pretty easily when investigating a .pcap file
	- `zeek -C -r sample.pcap local`
	- Also check out `/opt/zeek/share/zeek/policy/protocols/ftp/*`
		- Perhaps `detect-bruteforcing.zeek`
		- **This script is proper**
		- More information on prebuilt scripts, frameworks are in Zeeks online books (https://docs.zeek.org/en/master/frameworks/index.html)

Loading Specific Scripts
- Identifying the script path
- One now has the ability of loading a specific script, or a framework of them

Zeek Scripts and Frameworks
https://docs.zeek.org/en/master/frameworks/index.html
- 15+ frameworks that can help analysts to discover the different events of interest

- File Framework | Hashes
	- Not all framework functionalities are intended to be used in CLI
	- The majority of them are used in scripting
	- You can see the usage of a framework in scripts by calling a specific framework:
		- `load @ $PATH/base/frameworks/framework-name`
		- `@load /opt/zeek/share/zeek/policy/frameworks/files/hash-all-files.zeek`

	- Frameworks depend on scripts
	- `hash-all-files.zeek`
		```zeek
		@load base/files/hash
		event file_new(f: fa_file)
		{
		Files::add_analyzer(f, Files::ANALYZER_MD5);
		Files::add_analyzer(f, Files::ANALYZER_SHA1);
		Files::add_analyzer(f, Files::ANALYZER_SHA256);
		}
		```
		- `cat files.log`
	- You can either load the script into your own script, or call the script when investigating a .pcap file. Up to you with what you want to do achieve

- File-Framework | Extract Files
	- This framework can extract the files transferred in a given .pcap file
		- `@load /opt/zeek/share/zeek/policy/frameworks/files/extract-all-files.zeek`
			- an extract_files folder is created which will house the individual files within
			- `ls -l | nl`
				- Show the files numbered in a list
			- `file ./* | nl`
				- Will show what each file is in a numbered list :) 
		- `6	-rw-r--r-- 1 root   root   2437120 Jan 26 02:25 extract-1561667899.060086-HTTP-FOghls3WpIjKpvXaE`
		- The naming convention here consists of four values that come from `conn.log` and `files.log`, default "extract" keyword, timestamp value (`ts`), protocol (`source`), and connection ID (`conn_uids`). 
		- `cat files.log | zeek-cut fuid conn_uids tx_hosts rx_hosts mime_type extracted | nl`
			- The mime types can be handy here as it will show you the file type, ie if it's a text/plain file, msword file and so won
				- Well it can show more human-friendly terminology anyway
		- Some correlation between the different logs!
			- `grep -rin CNH24M1xFbLPRgxXfa * | column -t | nl | less -S`
			- Will search for the given value across all files in the working directory/pwd - in this case, the .log files
			- Will reference which file it had picked up the given search-variable in

- Notice-Framework | Intelligence
- https://docs.zeek.org/en/master/frameworks/intel.html
- https://docs.zeek.org/en/current/scripts/base/frameworks/intel/main.zeek.html#type-Intel::Type
- `@load /opt/zeek/share/zeek/policy/frameworks/intel/seen`
- `@load /opt/zeek/share/zeek/policy/frameworks/intel/do_notice.seek`
	- This framework can work with data feeds to process and correlate events and identify anomalies. 
	- This framework requires a feed to match and create alerts from the network traffic
	- Source location
		- `/opt/zeek/intel/zeek_intel.txt`
	- **Two critical points**:
		- 1. The source file has to be tab-delimited
		- 2. You can manually update the source and adding extra lines doesn't require any re-deployment
		- However
			- If you delete a line from the file, you will need to re-deploy the Zeek instance
		- Example for in the script just after @loading frameworks:
			- `redef Intel::read_files += { "/opt/zeek/intel/zeek_intel.txt" };`

- Package Manager (`zkg`)
- https://github.com/zeek/packages
- https://packages.zeek.org/
	- Needs **root** 
	- Zeek Package Manager helps users install third-party scripts and plugins to extend Zeek functionalities with ease
	- It's installed with Zeek and available with the `zkg` command
	- One can:
		- Install
		- Load
		- Remove
		- Update
		- Create packages
	- `zkg install package_path`
		- Install a package
			- `zkg install zeek/j-gras/zeek-af_packet-plugin`
	- `zkg install git_url`
		- Install a package
			- `zkg install https://github.com/corelight/ztest`
	- `zkg list`
		- List installed package
	- `zkg remove`
		- Remove installed package
	- `zkg refresh`
		- Check version updates for installed packages
	- `zkg upgrade`
		- Update installed packages
- Usage Approaches
	- First:
		- Using the packages as frameworks and calling specific package path/directory per usage (like we've covered here already)
	- Second:
		- Most common approach
		- Calling packages from a script with the `@load` method 
	- Third:
		- Calling their package names, this only works for packages installed with the `zkg install` method. 
- Packages | Cleartext Submission of Password
	- `zeek-sniffpass`
- Packages | Geolocation Data
- `zeek -Cr pcap.pcap geoip-conn`
- Depends on GeoLite2-City.mmdb database which is created by MaxMind
- ***`sumstats-counttable.zeek`***
	- Have saved this locally as a reminder to check it out in more depth
	- Real clean way to summarise 