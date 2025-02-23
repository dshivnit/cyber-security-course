https://tryhackme.com/room/irdifficultiesandchallenges

"These challenges often necessitate a nuanced and adaptive methodology to overcome and lead effective IR operations" 

Critical Components
- Organisational Culture
- Resource Limitations
- Data Visibility
- Storage Retention
- Anti-Forensics
- Human Error

Organisational Culture
- A culture that values and prioritises a coordinated response is crucial for prioritising, responding to, and learning from incidents
	- The recruitment process of personnel during an incident
	- Communication and coordination challenges
	- The role bureaucracy plays in decision-making
	- Mechanisms for incident reporting
- Personnel
	- Often, urgency around an incident that has been detected requires a rapid response - needing a specialised team and SMEs (Subject Matter Experts), who would be able to assemble and take appropriate action.
	- Without a streamlined process for requesting the necessary personnel, the organisation becomes more at risk for prolonged response times and the escalation of incidents. 
		- This deficiency becomes even more apparent outside regular business hours when personnel availability is limited
	- IT/Security Teams do not operate independently
		- Other groups and departments own applications, data, and other resources that IT would otherwise manage and secure - these other groups are stakeholders in the organisation. 
		- It's essential to involve relevant stakeholders in the planning process for security events and have them actively involved and informed in the resolution process
		- Especially when various stakeholders are off-duty, it is imperative to have an incident response plan in place so that the IR lead will be able to contact relevant key personnel in these other departments to get them on board (regardless if it is outside operating hours) - thus integrating a cross-functional IR team ensures that technical personnel from all relevant sides of the organisation can consult and assess the team's options and impact
	- IR Retainers
		- It's a proactive strategy for teams to consider the option of retainers in their incident response planning.
		- These are pre-negotiated agreements with external cyber security SMEs and specialised teams who are on standby to assist in the event of a security incident
		- Having an IR Retainer ready to be activated can significantly expedite assembling a response team when a critical incident occurs and allow organisations to tap into a broader pool of experts

Communication
- Addressing communication challenges before and during incidents is crucial for an effective and coordinated response
- The multiple communication channels teams have available can sometimes lead to indecision and disconnection among team members
- An essential early step in the IR lifecycle is establishing the team's open communication channels
	- This step focuses the team's reporting within an agreed-upon place, such as a Slack or Teams channel or a conference call bridge
- A maintained up-to-date contact list of all stakeholders **must** be kept.
	- Key personnel should be outlined in this list, such as the CIO, CISO, Head of InfoSec, and other internal response team stakeholders
		- (anyone relevant)
	- Depending on the severity of the incident, this list should also contain other stakeholders such as from departments like HR, Public Affairs, Legal Teams (and so on). 
	- In some situations, external resources such as data or system owners, law enforcement and government entities like the US-CERT (United States Computer Emergency Readiness Team) may also need to be included on the incident's location and scope.
- Preparing alternative out-of-band communication methods is essential during incident planning
	- Important if the scope of the incident or compromise encompasses the agreed-upon communication method itself - as attackers might be able to eavesdrop and gain awareness of the incident response strategy. 
	- Be cautious, and assume that threat actors can intercept communications until you have confidence that your regular communication channels are not compromised. 
	- Communication tools such as Signal or other similar messaging channel platforms serve as effective out-of-band  communication as they operate independently of the corporate network, offering a layer of separation that can be crucial during an incident
- Situation Reports (SITREPs)
	- SITREPs are pivotal in proactively engaging with key stakeholders and establishing a unified source of truth regarding risks. 
	- Organisations often overlook the significance of timely progress updates and prioritise technical aspects over communication
	- An effective SITREP includes a clear summary of the incident for *clear* understanding - it should summarise and track critical tasks and their status between each team. 
	- The report should end by planning when stakeholders expect the next update for transparency and accountability. 

Bureaucracy
- Organisational bureaucracy can pose challenge for IR teams
	- ie - a non-agile decision-making structure, characterised by multiple layers of hierarchy, can often delay when quick and decisive actions are required. 
	- Obtaining necessary approvals and authorisations for performing various remediation or mitigation actions can be time-consuming, further allowing the impact of the incident to escalate
- Emphasising IR's strategic importance in protecting organisational assets and company reputation becomes crucial in driving this cultural shift and must be done before an incident occurs during the **preparation phase** of the IR cycle.
- Recognising that delays in decision-making will have severe consequences for the organisation as a whole can help remove bureaucratic obstacles and create an environment conductive to swift decision-making when required
- This will involve reevaluating existing protocols, discussing with stakeholders to eliminate redundant approval processes, and empowering IR teams to act decisively in the face of evolving threats
- By demonstrating impact and framing incident response as not just a reactive measure but also a **proactive measure**, executives and decision-makers can be more inclined to provide the necessary resources and attention to strengthen the organisation's overall security posture. 

Incident Reporting Mechanisms
- The lack of a streamlined and efficient reporting mechanism can lead to significant delays or a complete lack of incident detection
	- Several techniques can be deployed to mitigate these challenges, such as implementing automated reporting tools (phishing or other security reporting tools), establishing clear reporting channels, and conducting regular security awareness training to ensure timely and accurate incident reporting. 
- Building a cyber-aware culture is often an organisation's greatest defence by instilling a sense of empowerment and understanding in employees
- By demonstrating the direct link between individual actions and the overall cyber security posture of the organisation, a culture that inherently values security and incident handling can thrive. 

Resource Constraints
- A significant challenge faced by IR teams is the need for more 
	- Funding
	- Budget
	- Personnel
- Budget constraints will often affect the acquisition of security tools and infrastructure necessary for adequate incident response
- As discussed previously, a shortage of personnel can aggravate these issues. 
- Making calculated trade-offs and compromises where possible is crucial for the success of IR teams
- Shortage of Personnel
	- This can create significant challenges that affect IR capabilities
		- Increased workloads - leading to burnout and greater potential for human investigation errors
	- When the volume of incident handling takes precedence out of necessity, the quality often suffers - and crucial considerations may be overlooked
		- This can lead to missed opportunities to address underlying issues, leading to the escalation of incidents and more significant consequences later on
	- IR Teams will often require diverse skill sets - and the lack of specialise expertise in areas such as log analysis, malware analysis, and network forensics can hinder the quality and depth of investigations. 
	- Budget constraints limit training opportunities for staff, leaving team members without the specialist skills to address evolving threats.
	- Cross-training Programs
		- Foster a culture of continuous learning, and establish knowledge-sharing opportunities
	- Outsourcing certain IR aspects to specialised providers can help supplement in-house capabilities, further advocations for increased budget allocations by demonstrating the value of a robust incident response team are also crucial for addressing these staffing needs at the top level
		- Organisations can proactively establish IR Retainer contracts to assist in the event of a security incident
		- It's important to acknowledge that security incidents are typically not constant occurrences - and when they do happen, there is a sudden surge in workload
			- This can significantly impact incident responders.
		- An effective strategy will be to activate retainers to consult with third-party service provider expertise to relieve internal team's workload for an effective response.

Inadequate Tooling
- Budget constraints can affect the available tooling that would contribute to the overall efficacy of an IR's teams capabilities. 
- Dependency on outdated software can compromise the IR process - legacy tools would normally lack the capability to combat evolved threat actors
	- There can also be an indirect cost implication with teams building makeshift solutions to counter threats when they could have invested in a robust tool set that is already available.
- Open-source tooling
	- Can be a cost-effective alternative to address budget constraints
	- Prioritising tool investment based on specific needs or areas according to the organisation's threat model optimises resource utilisation
- Cloud solutions are an option that can offer scalability without a high upfront cost.

Maximising Resources
- Risk-based prioritisation is when available IR resources within an organisation are maximised 
- Conducting a comprehensive risk assessment will identify and help prioritise critical assets, allowing teams to allocate resources based on the severity of identified risks
- Strategic outsourcing of specific functions can also optimise resource allocation
- Identifying non-core functions or specialised tasks suitable for outsourcing ensures that internal teams can focus on core security responsibilities
	- Ensure that outsourced operations align with security and compliance requirements
- The key element in resource optimisation is fostering a versatile team through cross-training and supporting skill development
- By providing team members with opportunities to enhance their skills, organisations can maximise the effectiveness of their cyber security personnel

Data Visibility
- Data visibility and storage retention challenges are also faced by IR Teams
- Many variables can contribute to decreased visibility, like:
	- Asset proliferation and distributed evidence
	- Complexities of data retention
	- Compliance regulations
	- Physical and logical constraints
- Asset Proliferation and Data Retention
	- The growing state of digital assets across many different organisational environments poses an inherent challenge for IR teams
	- Complex IT infrastructure with cloud services, IoT devices, and hybrid working environments - evidence that is relevant to an incident is often distributed across many systems and environments.
		- This makes it challenging for IR teams to quickly and comprehensively identify, analyze, and contain security incidents
	- Utilising a robust asset management system helps maintain an up-to-date inventory of assets across diverse environments
		- Additionally, using automated discovery tools and centralised asset repositories enables IR teams to quickly identify and track these ever-changing assets. 
		- Along with asset discovery - deploying host-based EDR solutions will enhance the real-time and centralised monitoring, providing visibility into the activities and collecting evidence relevant to security incidents
	- Classifying necessary evidence is crucial to effectively managing incidents, it is essential to approach evidence collection strategically and in a scalable manner
		- Gathering only the necessary evidence that helps responders swiftly understand the actions of the threat actor
	- In many cases - recovery efforts take precedence, where responders prioritise restoring the affected hosts before forensic evidence essential to the attacker's intrusion timeline can be collected. 

Data Retention and Legal Compliance
- Retaining extensive logs is crucial for post-incident analysis and compliance purposes
- This process can also introduce storage capacity and cost challenges
- Striking the correct balance between retaining enough data to conduct thorough investigations, identifying baselines, and ensuring compliance with legal frameworks like GDPR and HIPAA requires a nuanced approach
	- ie PCI DSS is a security standard for cardholder data collection 
	- Entities that collect cardholder data must keep an audit trail for at least one year and at least three months of data must be available be available for analysis. 
	- HIPAA on the other hand is a privacy act that protects an individual's collected medical records and identifiable health information. 
	- HIPAA compliance generally requires the retention of data for up to six years. As such organisations must be proactive in planning engagement with regulators during incident management.
- A common pitfall that IR's have faced is the lack of early engagement with legal counsel - who can introduce necessary risk to the overall response effort. 
	- Engaging with counsel (whether it be internal or external) early in the response is crucial (*I'd say early in the response plan phase as well*)
	- Organisations may fall short of meeting regulatory and compliance regulations without sound legal advice/guidance or inadvertently share excessive information with external parties
- Deploying intelligent data retention policies involves classifying data based on **function, criticality, and regulatory compliance.** 
- Automated tools for data lifecycle management with SIEM solutions or long-term solutions can allow teams to retain critical information while effectively purging non-essential data
- Many cloud providers offer the ability for data classification and nuanced retention and immutability policies 
	- This can assist in ensuring compliance and also optimises storage resources

Physical and Logical Constraints
- Physically dispersed infrastructures, remote work scenarios, and the increasing implementation of third-party services all contribute to the difficulty of quickly accessing and analyzing critical data during an incident
- The limitations of existing storage solutions, bandwidth constraints, and sheer volume of data generated in modern environments further strain the capabilities of IR teams - impeding the ability to respond swiftly and effectively
- Cloud-based storage and collaboration tools can be solutions to overcome physical and logical constraints
	- Cloud storage enhances scalability and accessibility - which will allow IR teams to store and process large volumes of data more efficiently
	- Adopting collaborative incident tracking software (like JIRA, ServiceNow, Tello, Asana etc) allows seamless communication and coordination among dispersed team members during incident response, overcoming geographical and logistical barriers. 

Anti-Forensics
- Anti-forensics refers to a threat actor's techniques and strategies to undermine forensic investigations
	- These techniques erase, hide or manipulate evidence - which makes it difficult for investigators to work with
- Anti-forensic methods can be found at various stages of the IR process, including interfering with data acquisition, hot and cold analysis, and reporting
- Some anti-forensic methods:
	- Data deletion
	- Encryption
	- Steganography
	- Log manipulation
	- Memory forensics evasion
	- Physical hardware manipulation
- Data Deletion
	- Various secure file deletion operations can be employed to overwrite existing data with random patterns multiple times, making it difficult or nearly impossible for standard data recovery methods to reconstruct the original information
	- The manipulation and reformatting of storage devices are basic yet effective measures to interfere with evidence collection
	- Metadata Stripping
		- These techniques can be used as an additional layer of obfuscation
		- Metadata is often embedded within files - which serve information about the file itself (creation and modification dates, author details, and other contextual attributes)
		- Stripping or removing this metadata from files can further hinder the investigation process by removing valuable contextual information that establishes the origin and history of a file
	- Regularly backing up critical data to independent storage ensures a restorable copy exists even if data is deleted. 
	- Employing endpoint security and file integrity monitoring adds another layer of defense by detecting unauthorised file access and modifications to sensitive data
	- File carving
		- File carving is a data recovery process that attempts to extract deleted information by searching for specific file signatures or patterns within the raw data of a storage device and extracting files based on these patterns
		- It is powerful, effective of a technique even when file system metadata is unavailable or altered
		- It isn't a silver bullet though, and depends entirely on the accuracy of the file signature detection
	- Tools like `exiftool` can be used to view a file's metadata, however, attackers can use the same tool (or similar) to strip and remove a file's metadata or insert erroneous data to confuse analysts
		- `exiftool -all= filename.pdf`
			- This command will strip away all metadata from the filename.pdf file

Encryption
- Encryption often serves as a protective measure to secure sensitive data and communications by converting plaintext information into ciphertext using keys and algorithms
- While encryption primarily enhances security, threat actors can exploit it as an anti-forensic technique to impede incident response investigations
	- Such as in the event that threat actors encrypt disks or files to block access to stored data
- To counteract threat actors using encryption, organisations should first ensure that they maintain regular and secure backups of critical data, up-to-date backups ensure that systems can be restored in the event of data and file encryption
- To mitigate the potential for unauthorised data encryption, it is essential to implement the **principle of least privilege**. 
	- Restricting user access to the minimum required for their roles will reduce the likelihood of unauthorised access and potential encryption of sensitive files. 
- Deploying monitoring and detection tools aids in identifying unusual activities on networks and endpoints, even if they involve encrypted data. 

Steganography
- A technique used to hide or embed information within other non-secret data - like images, audio files, or text - in a way that is not readily apparent
- The primary goal of steganography is to conceal secret information rather than secure it through encryption
- Common methods include:
	- Hiding data within the least significant bits of image pixels
	- Altering the spacing between words or characters in a text
	- Embedding information in the frequency components of audio signals
- Combating steganography techniques require proactive measures and implementing detection techniques
	- Regular traffic monitoring, content inspection, and behavioural analysis help identify anomalies and hidden payloads within files
	- File Integrity Monitoring tools can detect unauthorised file changes as an additional defense layer
- Steganalysis - is the process of detecting and uncovering the hidden information within files. It involves analyzing statistical properties, frequency distributions and other patterns within files to identify anomalies indicative of hidden content
- Tools like Outguess (https://www.rbcafe.com/software/outguess/)  can aid in the identification and analysis of hidden content within images and different file types

Log Manipulation
- This term refers to the unauthorised or malicious alteration of log files within a computer system or network
- Can take various forms - such as deleting or modifying log entries, altering timestamps, or simply injecting false information into the logs
- Attackers manipulate records to conceal their activities, evade detection or mislead investigators during incident response
- Enforcing **centralised log management** is key to mitigating log manipulation concerns.
- This involves:
	- Securing the storage of log files through access controls and encryption
	- Establishing clear log retention policies and implementing integrity checks
	- Performing regular review and analysis of logs - either manually or with automated tools - to identify missing data or timeline anomalies

Memory Forensics Evasion
- Threat actors have incorporated anti-forensic techniques within malware payloads to obstruct analysis by concealing malicious memory areas within a system's volatile storage
- These techniques can consist of manipulating kernel structures, or, through process injection for example
	- Where malware is inserted into the allocated memory of space of a legitimate, trusted process
	- By injecting into the memory of a trusted process, malicious code can execute without triggering traditional signature-based detection solutions and evade static analysis
- These techniques make identifying the malware much more challenging for security teams and detection tools
- Mitigating various forms of process injection poses a big challenge for teams, due to its legitimate integration into the Windows ecosystem
	- Security teams can, however, proactively impede specific types of arbitrary code execution using application control solutions such as **AppLocker** and **Application Control** for Windows
- On a broader scale, identification efforts involve looking for anomalies such as the lack of command-line logs or artifacts of network traffic where there shouldn't be
- Focusing on high-value processes can identify suspicious behaviour
	- `lsass.exe` for example - is a commonly targeted and sensitive process that warrants meticulous attention during investigations

Physical Hardware Manipulation
- The tampering of physical hardware and its components
- Attackers can disrupt normal functioning of the system and obfuscate evidence, making it challenging for investigators to reconstruct events accurately
	- One method involves insertion of malicious hardware devices, such as rogue USB devices or hardware implants
		- These devices can exfiltrate data, inject malicious code, or create covert command-and-control communication channels
	- Hardware component substitution is another technique where legitimate hardware components are replaced with compromised ones
		- A NIC being replaced with a manipulated counterpart designed to redirect or intercept network traffic
		- This manipulation can enable attackers to control communication flows and evade detection by traditional network monitoring tools
- In some cases attackers may physically destroy hardware to eradicate evidence or divert forensic investigations
- The risks associated with physical hardware manipulation should be mitigated by enforcing strict physical security protocols and limiting access to areas housing critical hardware components
- Maintaining a comprehensive hardware inventory also enhances the detection of any unauthorised device or system alterations

Human Error
- Missteps in following established protocols, judgement errors (like mischaracterising the severity of an incident) and bias can result in in accurate and delayed resolution
- These delays could allow for adversaries to persist within networks, increasing the attack surface and potentially leading to a more severe incident or loss of valuable evidence
- Sources of Human Error
	- Lack of proper training
		- On tools, processes - can leave team members ill-equipped to handle evolving threats and sophisticated attack scenarios
	- Communication Breakdowns
		- Whether due to unclear processes or ineffective collaboration, can further exacerbate the frequency of errors
	- Cognitive biases
		- Such as over-reliance on past experiences or a tendency to underestimate specific threats, can introduce weaknesses in response strategies and uncomprehensive analysis
	- To mitigate the impact of human errors, incident response teams can implement the following strategies:
		- Continuous and cross-disciplinary training programs:
			- Ongoing and diverse training initiatives designed to keep incident response team members abreast of the latest threat landscapes and response techniques
			- Goal is to ensure a well-rounded skill set among team members
		- Clear communication protocols
			- Established guidelines and procedures that facilitate unambiguous communication within the incident response team
			- Help to reduce misunderstandings and promote a coordinated and efficient response during security incidents
		- Decision-making Frameworks
			- Refer to structured approaches or methodologies designed to guide incident response teams in making effective decisions during high-pressure and complex situations
			- Aim is to minimise the risk of judgement errors and emphasise reliance on facts and evidence
		- Post-incident Reviews or Postmortems
			- Evaluative processes conducted after an incident to analyse the response, identify shortcomings, and foster a culture of learning from mistakes
			- The objective is to turn each incident into an opportunity for improvement, thereby enhancing the overall resilience of the incident response team