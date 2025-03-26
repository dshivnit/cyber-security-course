https://tryhackme.com/room/threatmodelling

Overview
- Threat modelling is a systematic approach to **identifying**, **prioritising**, and **addressing potential security threats** across the organisation
- Through the simulation of possible attack scenarios and the assessment of existing vulnerabilities of the organisation's interconnected systems and applications, threat modelling enables organisations to develop proactive security measures and make informed decisions about resource allocation
- Threat modelling aims to reduce an organisation's overall risk exposure by identifying vulnerabilities and potential attack vectors
	- Allowing for adequate security controls and strategies
- Threat modelling is essential for constructing a robust defence strategy against the ever-evolving cyber threat landscape

Threat, Vulnerability and Risk
- Threat
	- Any potential occurrence, event, or actor that may exploit vulnerabilities to compromise information confidentiality, integrity, or availability
	- Various forms such as cyber attacks, human error, or natural disasters for example
	- ie - Occurrence of someone breaking inside your home and taking all your belongings
- Vulnerability
	- A weakness or flaw in a system, application, or process that may be exploited by a threat to cause harm 
	- It may arise from software bugs, misconfiguration, or design flaws for example
	- ie Weaknesses in your home security, such as broken locks or open windows
- Risk
	- The possibility of being compromised because of a threat taking advantage of a vulnerability
	- A way to think about how likely an attack might be successful and how much damage it could cause
	- ie Likelihood of being burglarised due to living in a neighbourhood with a high crime rate or a lack of an alarm system

High-level Process of Threat Modelling
- 1. Defining the Scope
	- Identify the specific systems, applications, and networks in the threat modelling exercise
- 2. Asset Identification
	- Develop diagrams of the organisation's architecture and its dependencies
	- Also essential to identify the importance of each asset based on the information it handles, such as customer data, intellectual property, and financial information
- 3. Identify Threats
	- Identify potential threats that may impact the identified assets, such as cyber attacks, physical attacks, social engineering, and insider threats
- 4. Analyse Vulnerabilities and Prioritise Risks
	- Analyse the vulnerabilities based on the potential impact of identified threats in conjunction with assessing the existing security controls
	- Given the list of vulnerabilities, risks should be prioritised based on their likelihood and impact
- 5. Develop and Implement Countermeasures
	- Design and implement security controls to address the identified risks, such as implementing access controls, applying system updates, and performing regular vulnerability assessments
- 6. Monitor and Evaluate
	- Continuously test and monitor the effectiveness of the implemented countermeasures and evaluate the success of the threat modelling exercise
	- An example of a simple measurement of success is tracking the identified risks that have been effectively mitigated or eliminated

Collaboration with Different Teams
- The process above involves many tasks, so it will be important to have multiple teams collaborating together
- Each unit will offer valuable skills and expertise, helping improve the organisation's security posture
- By collaborating, organisations can effectively address and align the security efforts needed to build a better defence. 
- Some teams perhaps could be:
	- Security Team
		- Overarching team of red and blue teams
		- This team will typically lead the threat modelling process, providing expertise on threats, vulnerabilities, and risk mitigation strategies
		- They also ensure security measures are implemented, validated, and continuously monitored
	- Development Team
		- Responsible for building secure systems and applications
		- Their involvement ensures that security is always incorporated throughout the development lifecycle
	- IT and Operations Team
		- IT and Operations manage the organisation's infrastructure
		- Including networks, servers, and other critical systems
		- Their knowledge of network infrastructure, system configurations, and application integrations is essential for effective threat modelling
	- Governance, Risk and Compliance Team
		- The GRC Team is responsible for organisation-wide compliance assessments based on industry regulations and internal policies
		- They collaborate with the security team to align threat modelling with the organisation's risk management objectives
	- Business Stakeholders
		- Provide valuable input on the organisation's critical assets, business processes, and risk tolerance
		- Their involvement ensures that the efforts align with the organisation's strategic goals
	- End Users
		- As direct users of a system or application, end users can provide unique insights and perspectives that other teams may not have 
		- Enabling the identification of vulnerabilities and risks specific to user interactions and behaviours

Attack Trees
- Creating an attack tree is another good way to identify and map threats
- A graphical representation used in threat modelling to systematically describe and analyse potential threats against a system, application or infrastructure. 
- Provides a structured, hierarchical approach to breaking down attack scenarios into smaller components
	![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/ab10d8571dca42dfcab63c952c436413.png)
	- The root node in this example outlines the attackers primary goal - being to gain unauthorised access to sensitive data.
	- Then you have the different high-level strategies an attacker might do to achieve that goal
	- Then each of those strategies is further broken down detailing specific techniques that the attacker might choose to employ
	- Attack paths may be seen which will depict the possible routes, or sequence of vulnerabilities that a threat actor can exploit to achieve their goal 
	- Attack paths are pretty much chains of vulnerabilities that are interconnected

MITRE ATT&CK Navigator
- https://mitre-attack.github.io/attack-navigator/
- Great framework for threat modelling as you can filter down various components to fit the modelling's requirements

DREAD Framework
- A risk assessment model developed by Microsoft to evaluate and prioritise security threats and vulnerabilities
- Damage
	- The potential harm that could result from the successful exploitation of a vulnerability
	- Includes data loss, system downtime, reputational damage 
- Reproducibility
	- The ease with which an attacker can successfully recreate the exploitation of a vulnerability
	- A higher reproducibility score suggests that the vulnerability is straightforward to abuse, posing a greater risk
- Exploitability
	- The difficulty level involved in exploiting the vulnerability considering factors such as technical skills required, availability of tools or exploits, and the amount of time it would take to exploit the vulnerability successfully
- Affected Users
	- The number or portion of users impacted once the vulnerability has been exploited
- Discoverability
	- The ease with which an attacker can find and identify the vulnerability considering whether it is publicly known or how difficult it is to discover based on the exposure of the assets (publicly reachable, or in a regulated environment)

- Damage - How bad would an attack be?
- Reproducibility - How easy is it to reproduce the attack?
- Exploitability - How much work is it to launch the attack?
- Affected Users - How many people will be impacted? 
- Discoverability - How easy is it to discover the vulnerability?

- The DREAD Framework is an opinion-based model that heavily relies on an analyst's interpretation and assessment
- However, the reliability of this framework can still be improved by following some guidelines
	- 1. Establish a standardised set of guidelines and definitions for each DREAD category that provides a consistent understanding of how to rate vulnerabilities
		- This can be supported by providing examples and scenarios to illustrate how scores should be assigned under various circumstances
	- 2. Encourage collaboration and discussion among multiple teams. Constructive feedback from different members aids in justifying the assigned scores, which can lead to a more accurate assessment
	- 3. Use the DREAD framework with other risk-assessment methodologies and regularly review and update the chosen methods and techniques to ensure they remain relevant and aligned with the organisation's needs

- The DREAD framework is mainly used for Qualitative Risk Analysis - rating each category from one to ten based on a subjective assessment and interpretation of the questions above

STRIDE Framework
- Threat modelling methodology also developed by Microsoft - which helps identify and categorise potential security threats in software development and system design

- Spoofing
	- Unauthorised access or impersonation of a user or system 
	- Policy violated - Authentication
- Tampering
	- Unauthorised modification or manipulation of data or code
	- Policy violated - Integrity
- Repudiation
	- Ability to deny having acted, typically due to insufficient auditing or logging
	- Policy violated - Non-repudiation
- Information Disclosure
	- Unauthorised access to sensitive information, such as personal or financial data
	- Policy violated - Confidentiality
- Denial of Service
	- Disruption of the system's availability, preventing legitimate users from accessing it
	- Policy violated - Availability 
- Elevation of Privilege
	- Unauthorised elevation of access privileges, allowing threat actors to perform unintended actions
	- Policy violated - Authorisation

- Examples
	- Spoofing
		- Sending an email as another user
		- Creating a phishing website mimicking a legitimate one to harvest user credentials
	- Tampering
		- Updating the password of another user
		- Installing system-wide backdoors using an elevated access
	- Repudiation
		- Denying unauthorised money-transfer transactions, wherein the system lacks auditing
		- Denying sending an offensive message to another person, wherein the person lacks proof of receiving one
	- Information Disclosure
		- Unauthenticated access toa  misconfigured database that contains sensitive customer information
		- Accessing public cloud storage that handles sensitive documents
	- Denial of Service
		- Flooding a web server with many requests, overwhelming its resources, and making it unavailable to legitimate users
		- Deploying a ransomware that encrypts all system data that prevents other systems from accessing the resources that compromised server needs 
	- Elevation of Privilege
		- Creating a regular user but being able to access the administrator console
		- Gaining local administrator privileges on a machine by abusing unpatched systems

- Threat Modelling with STRIDE
	- It is essential to integrate the six threat categories into a systematic process that effectively identifies, assesses, and mitigates security risks. Following is a high-level approach to incorporating STRIDE:
		- 1. System Decomposition
			- Break down all accounted systems into components, such as applications, networks, and data flows. 
			- Understand the architecture, trust boundaries, and potential attack surfaces. 
		- 2. Apply STRIDE Categories
			- For each component, analyse its exposure to the six STRIDE threat categories.
			- Identify potential threats and vulnerabilities related to each category
		- 3. Threat Assessment
			- Evaluate the impact and likelihood of each identified threat.
			- Consider the potential consequences and the ease of exploitation and prioritise threats based on their overall risk level. 
		- 4. Develop Countermeasures
			- Design and implement security controls to address the identified threats tailored to each STRIDE category. 
			- For example - to enhance email security and mitigate spoofing threats, implement DMARC, DKIM and SPF
				- Which are email authentication and validation mechanisms that help prevent email spoofing, phishing and spamming
		- Validation and Verification
			- Test the effectiveness of the implemented countermeasures to ensure they effectively mitigate the identified threats. 
			- If possible, conduct penetration testing, code reviews, or security audits
		- Continuous Improvement
			- Regularly review and update the threat model as the system evolves and new threats emerge. 
			- Monitor the effective countermeasures and update them as needed
		- 