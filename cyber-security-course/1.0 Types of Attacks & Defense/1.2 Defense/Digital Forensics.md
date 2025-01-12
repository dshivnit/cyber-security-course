https://tryhackme.com/r/room/digitalforensicsfundamentals

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
	- 
