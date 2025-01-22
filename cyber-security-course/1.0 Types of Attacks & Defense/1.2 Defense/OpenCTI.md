https://github.com/OpenCTI-Platform/opencti
https://tryhackme.com/r/room/opencti

- An open-source threat intelligence platform
- Designed to provide organisations with the means to manage CTI through the storage, analysis, visualisation and presentation of threat campaigns, malware and IOCs
- Developed by the collaboration of the French National Cybersecurity Agency (ANSSI) https://cyber.gouv.fr/en
- The platform's main objective is to create a comprehensive tool that allows users to capitalise on technical and non-technical information while developing relationships between each piece of information and its primary source. 
- It can use the MITRE ATT&CK framework to structure the data
- It can be integrated with other threat intel tools such as MISP and TheHive. 

OpenCTI Data Model
- The main knowledge schema that OpenCTI uses to structure data, is the Structured Threat Information Expression (**STIX2**) standard(s)
- STIX is a serialised and standardised language format used in threat intelligence exchange. 
- It allows for the data to be implemented as entities and relationships
	- Effectively tracing the origin of the provided information
	- This data model below (from OpenCTI Public Knowledge Base via THM - OpenCTI lab) is supported by how the platform's architecture has been laid out. 
	- It gives an architectural structure for your know-how
![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5fc2847e1bbebc03aa89fbf2/room-content/3bbe38f3ae0edf761c9e0541a71d43ff.png)

The highlight services include:
- GraphQL API:
	- The API connects clients to the database and the messaging system
- Write Workers
	- Python processes utilised to write queries asynchronously from the RabbitMQ messaging system
- Connectors
	- Another set of Python processes used to ingest, enrich or export data on the platform.
	- These connectors provide the application with a robust network of integrated systems and frameworks to create cyber threat intelligence relations and allow users to improve their defence tactics. 
- According to OpenCTI, connectors fall into the following classes:
	- External Input Connector
		- Ingests information from external sources
			- CVE, MISP, TheHive, MITRE
	- Stream Connector
		- Consumes platform data stream
			- History, Tanium
	- Internal Enrichment Connector
		- Takes in OpenCTI entities from user requests
			- Observables enrichment
	- Internal Import File Connector
		- Extracts information from uploaded reports
			- PDFs, STIX2 import
	- Internal Export File Connector
		- Exports information from OpenCTI into different file formats
			- CSV, STIX2 report, PDF
- Connectors documentation - https://docs.opencti.io/latest/deployment/connectors/
- Data Model documentation - https://docs.opencti.io/latest/deployment/overview/

- The general day-to-day usage of OpenCTI would involve navigating through different entities within the platform to understand and utilise the information for any threat analysis. 