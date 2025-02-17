https://tryhackme.com/r/room/digitalforensicsfundamentals
https://tryhackme.com/room/introductoryroomdfirmodule

Digital Forensics Methodology
- NIST (National Institute of Standards and Technology) define a general process for every case. 
- NIST works on frameworks for different areas of technology, including cybersec, where they introduce the process of digital forensics in four phases:
	- Collection
		- Identifying all devices from which data can be collected is essential
		- Important to ensure that the original data isn't tampered with when collecting evidence, and maintaining proper documentation containing items' collected is important as well
	- Examination
		- Data would normally need to be filtered due to the extent of how much there can be and how much of it would be relevant in the case at hand
	- Analysis
		- Correlating the data with multiple devices and pieces of evidence to be able to draw conclusions
		- Aims to extract the activities relevant to the case chronologically
	- Reporting
		- Lastly, a detailed report is prepared
		- Contains the investigations methodology, detailed findings from collected evidence, and possibly recommendations in moving forward
		- This report would then be presented to law enforcement and executive management
		- Important to include executive summaries as part of the report, considering the level of understanding of all the receiving parties

Different types of Digital Forensics
- All with their own collection and analysis methodologies
	- Computer Forensics
		- The most common type
	- Network Forensics
		- Covers investigation beyond individual devices - the entire network, network traffic logs, etc
	- Database Forensics
		- Critical data stored in dedicated DBs
		- DB Forensics investigates any intrusion into these DBs that result in data modification or exfiltration
	- Memory Forensics
		- Physical memory - much deeper dive into seeing if anything can be recovered from it
	- Mobile Forensics
		- Call records, SMSs, GPS locations, etc
	- Malware Forensics
	- Email Forensics
		- Common communication method between professionals
	- Cloud Forensics
	- Disk Forensics

Evidence Acquisition
- Proper Authorisation
	- The Forensics Team should gain authorisation from the relevant authorities before collecting any data
	- Evidence collected without prior approval may be inadmissible in court
	- Evidence normally would contain private and sensitive data of an organisation or individual - sticking within the boundaries of the law is important in making sure that the Team have the proper authority and go-ahead to look into this data prior to doing so (ie a Search Warrant)
- Chain of Custody
	- Process for documenting the evidence owners
	- Chain of Custody document
		- Contains details on all of the evidence:
			- Description of the evidence (name, type, etc)
			- Name of individuals who collected the evidence
			- Date and time of collection
			- Storage location for each piece of evidence
			- Access times and the individual record who accessed the evidence
	- We don't want the said evidence to go walkies, now do we..
	- The Chain of Custody document can prove the integrity and reliability of the evidence admitted in court. 
- Use of Write Blockers
	- While collecting data from devices taken from a crime scene, or that are a part of an investigation - some of the tools that the Digital Forensics Team may use can inadvertently alter timestamps of the files being accessed from said evidence (like an HDD)
	- Using a Write Blocker can help prevent that from happening
	- Keeping the evidential HDD in its original state as the write blocker can block any alteration to the target device whilst investigating it

Windows Forensics
- Various OSs could be used - the THM I'm looking at right now is focusing on Windows, however:
- Disk Image
	- Taking a disk image of the device that is being investigated is important - as it will save the HDD contents in a state that it was in upon collection - thus the team(s) involved can make copies of it for further analysis and so on
- Memory Image
	- Contains data inside the RAM of the device being investigated
	- Memory image should be prioritised and taken first from the system (as it is volatile)
- Tools:
	- FTK Imager
		- Widely used tool for taking disk images of Windows OSs
	- Autopsy
		- Open-source digital forensics platform
		- Can import an acquired disk image into this tool, and it will carry out an extensive analysis of the image
			- Keyword search
			- Deleted file recovery
			- File metadata
			- Extension mismatch detection
			- and more
	- Dumpit
		- Offers the utility of taking a memory image from a Win machine
		- Creates memory images using CLI and few commands
		- Memory image can be taken in different formats
	- Volatility
		- Open-source tool for analysing memory images
		- Each artifact can be analysed using a specific plugin
		- Supports various OSs
	- There other tools (more to describe on this later)

DFIR - Digital Forensics and Incident Response
- Covers the collection of forensic artifacts from digital devices such as computers, media devices, and smartphones to investigate an incident
- Helps teams to identify footprints left by an attacker when a security incident occurs - use them to determine the extent of compromise in an environment, and restore the environment to the state it was before the incident occurred. 

- Finding evidence of attacker activity in the network and sifting false alarms from actual incidents
- Robustly removing the attacker, so their foothold from the network no longer remains
- Identifying the extent and timeframe of a breach
	- This helps in communicating with relevant stakeholders
- Finding the loopholes that led to the breach
	- What needs to be changed to avoid the breach in the future
- Understanding attacker behaviour to pre-emptively block further intrusion attempts by the attacker
- Sharing information about the attacker with the community

Digital Forensics
	- These professionals are experts in identifying forensic artifacts or evidence of human activity in digital devices
Incident Response
- Incident responders are experts in cybersecurity and leverage forensic information to identify the activity of interest from a security perspective
DFIR Professionals
- These pro's know about Digital Forensics and Cybersecurity and combine these domains to achieve their goals
- DFIR domains are often combined because they are highly interdependent
- DF takes its goals and scope from the IR process
- IR leverages knowledge gained from DF and defines the extent of the forensic investigation

Artifacts
- Artifacts are pieces of evidence that point to an activity performed on a system
- They are collected to support a hypthesis or claim about attacker activity

Evidence Preservation
- The integrity of evidence collected must be maintained
- There are best practices which have been established as standards in the industry
- Note - any forensic analysis contaminates the evidence
	- Evidence is first collected, and then write-protected
	- A copy of the write-protected evidence is then used for analysis
	- This process ensures that the original artifact(s) is not contaminated and remains safe while analyzing
- If the copy that is being investigated gets corrupted, then the team(s) can return and make a new copy from the original artifact(s)

Chain of Custody
- When evidence is collected, it must be made sure that it is kept in secure custody
- Any person(s) not related to the investigation must not possess the evidence, or it will contaminate the chain of custody of the evidence
	- Contaminated artifacts lessen the integrity of data and will weaken the case being built

Order of Volatility
- RAM for example
	- Is lost when the computer is shut down
- It is vital to understand the order of volatility of the different evidence sources to capture and preserve accordingly
- Prioritize!

Timeline Creation:
- Once artifacts have been collected and their integrity maintained
	- They need to be presented understandably to fully use the information contained in them
- A timeline of events needs to be created for efficient and accurate analysis
	- The timeline of events will put all activities in a chronological order
- Provides perspective to the investigation and helps collate information from various sources to create a story of how things happened

Tools
- Eric Zimmerman's
- https://ericzimmerman.github.io/#!index.md
	- A security researcher who has written a few tools to help perform forensic analysis on the Windows platform
- KAPE
- https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape
	- Kroll Artifact Parser and Extractor
	- Also by Zimmerman
	- Automates the collection and parsing of forensic artifacts and can help create a timeline of events
	- A live data acquisition and analysis tool which can be used to acquire registry data
	- Primarily CLI, but also with a GUI
	- 
- Autopsy
- https://www.autopsy.com/
	- Open-source forensics platform that assists in analyzing data from digital media like mobile devices, hard drives, and removable drives
	- Plugins can assist in speeding up the forensic process, extract and to present valuable information from raw data sources
- Volatility
	- Assists in performing memory analysis for memory captures from both Windows and Linux OSes
	- Can extract valuable information from the memory of a machine under investigation
- Redline
	- Incident response tool developed by FireEye
	- Gathers forensic data from a system and helps with collected forensic information
- Velociraptor
	- Advanced endpoint-monitoring, forensics, and response platform
	- Open-source, yet powerful
- FTK Imager

The Incident Response Process
- The NIST Handling Guide:
	- https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf
	- Preparation
	- Detection and Analysis
	- Containment, Eradication, and Recovery
	- Post-incident Activity
- SANS Handler's Handbook: (PICERL)
	- https://www.sans.org/white-papers/33901/
	- Preparation
		- Before an incident occurs
		- Ensuring everyone that would be involved is ready before an event
		- The right people, processes, and technology to prevent and respond to incidents
	- Identification
		- Incident is identified though indicators
		- Indicators are analysed for False Positives, then documented, and communicated to relevant stakeholders
	- Containment
		- Incident/threat is contained
		- Efforts to minimise incidents effects are carried out
		- Short and long-term fixes for containment of the threat based on the forensic analysis of the incident that will also be a part of this phase
	- Eradication
		- Threat is eradicated from the system/network
		- A proper forensic analysis must be ensured to be carried out and the threat effectively contained before eradication
		- If the entry point of the threat actor(s) on to the system is not mitigated, eradicated - then this is no good (lol)
	- Recovery
		- Services that had been disrupted are brought back to pre-incident status/conditions
	- Lessons Learned
		- A review of the incident is performed
		- The incident is documented, and steps are taken based on the findings from the incident to ensure that teams are better prepared for a next time should the incident occur again
