https://www.activeresponse.org/wp-content/uploads/2013/07/diamond.pdf

https://tryhackme.com/r/room/diamondmodelrmuwwg42

Developed by Sergio Caltagirone, Andrew Pendergast, and Christopher Betz in 2013

Event
- Defines discrete time-bound activity restricted to a specific **phase** where an adversary, **requiring** external **resources**, uses a **capability** and **methodology** over some **infrastructure** against a **victim** with a given **result**. 

Core Features:
- Adversary
- Infrastructure
- Capability
- Victim

Meta-Features:
- Timestamp
	- Both start and end
- Phase
- Result
- Direction
- Methodology
- Resources

Two additional components/axes:
- Social
- Political and Technology

Confidence Value
- Each event feature, whether it is a core or meta feature, has an associated **confidence value**.
- A function of multiple values
	- Such as the confidence of an analytical conclusion and/or the accuracy of a data source

 The model is shaped like a diamond. With four core features which are edge-connected. 
- Which represent their underlying relationships and are arranged in the shape of a diamond.
- An **Adversary** deploys a **Capability** over the some **Infrastructure** against a **Victim**. 

The Diamond Model can help explain to non-technical people, about what happened during an event, or any valuable information on the threat actor. 

Adversary
- An attacker, enemy, cyber threat actor, or hacker
- The people (or person) who stand behind a cyberattack
- There is a distinction between an adversary operator and a adversary customer
	- Knowing this distinction can help one understand intent, attribution, adaptability, and persistence by helping to frame the relationship between an adversary and victim pair
- Normally the Adversary core feature would be empty in the early stages of an attack, or discovery of a breach/attack
	- Utilising data from an incident or breach, signatures, and other relevant information can help one determine who the adversary might be
	- Knowing APTs, their TTPs, and so on (and there are many..!)
- Adversary Operator
	- The "hacker" or person(s) conducting the intrusion activity
- Adversary Customer
	- The entity that stands to benefit from the activity conducted in the intrusion. 
	- It might be the same person who stands behind the adversary operator, or it could be a completely separate person or group

Victim
- Target of the adversary
- Can be an organisation, a person, target email address, domain, and so on
- Differentiating between Victim Persona and the Victim Assets is important because they serve different analytic (or analytical?) functions
- There is always a victim in every cyberattack. Can be a target which can serve as an opportunity for threat actors to get a foothold in the system, and so on. 
- Victim Personae
	- The people and/or organisations being targeted and whose assets are being attacked and exploited
	- These can be organisation names, people names, industries, job roles, interests and so on
- Victim Assets
	- The attack surface and include the set of systems, networks, email addresses, hosts, IP addresses, social networking accounts and so on which the threat actor will direct their capabilities towards

Capability
- Known as the skill, tools, techniques used by the adversary in the event
- Highlights the adversary's TTPs
- Capability Capacity
	- All the vulnerabilities and exposures that the individual capability can use
- Adversary Arsenal
	- Set of capabilities that belong to an adversary
	- Combined capacities of an adversary's capabilities make it the adversary's arsenal
- The adversary must have required capabilities
	- Could be malware and/or phishing email development skills
- Or at least access to capabilities
	- Such as acquiring malware or ransomware as a service...

Infrastructure
- Known as software or hardware
- The physical or logical interconnections that the adversary uses to deliver a capability or maintain control of capabilities
- Example - a C2 (Command and Control Centre) and the results from the victim (Data Exfiltration)
- Infrastructure can also be IP addresses, domain names, email addresses, or even a malicious USB device found in the street that is being plugged into a workstation..
- **Type 1 Infrastructure:**
	- The infrastructure controlled or owned by the adversary
- **Type 2 Infrastructure**
	- The infrastructure controlled by an intermediary
	- Sometimes the intermediary might or might not be aware of it
	- This is the infrastructure that a victim will see as the adversary
	- Has the purpose of obfuscating the source and attribution of the activity
	- Includes malware staging servers, malicious domain names, compromised email accounts, and so on
- **Service Providers**
	- Organisations that provide services considered critical for the adversary availability of Type 1 and Type 2 infrastructures, for example, ISPs, domain registrars, and webmail providers

Event Meta Features
- These aren't required, but they can add information or intelligence to the event/scenario at hand
- Timestamp
	- The date and time of the event
	- Including when the event starts, and when it stops
	- Essential to determine patterns and group various activities together
		- ie, it was after-hours here in the country, but it could have been 'office hours' in another country (lol)
- Phase
	- The phases of an intrusion, attack, or breach.
	- "Every malicious activity contains two or more phases which must be successfully executed in succession to achieve the desired result" - Diamond model creators and the Axiom 4
	- Malicious activities do not occur as single events, but rather as a sequence of events
		- Such as the phases described in Lockheed Martin's Cyber Kill Chain, or the Unified Kill Chain and so on
- Result
	- Results and post-conditions of an adversary's operations will not always be known, or might have a high-confidence value when they are known - it is helpful to capture.
	- Event results can be captured as (for example) - success, failure, or unknown
	- Event results can be related to the CIA Triad, in which the pillar(s) affected can be outlined
	- Another addition can be documenting the post-conditions resulting from the event(s)
- Direction
	- Helps describe host-based and network-based events and represents the direction of the intrusion attack
	- The Diamond Model of Intrusion Analysis defines seven potential values for the Direction Meta-Feature. 
		- Victim-to-infrastructure
		- Infrastructure-to-victim
		- Infrastructure-to-infrastructure
		- Adversary-to-infrastructure
		- Infrastructure-to-Adversary
		- Bidirectional
		- Unknown
- Methodology
	- Will allow an analyst to describe the general classification of intrusion, for example - phishing, DDoS, breach, port scan
- Resources
	- According to the Diamond Model - every intrusion event needs one or more external resources to be satisfied to succeed
	- Examples can be - software (OSs, virtualisation software, the Metasploit framework, knowledge (hmm, external? I guess it could be?), information, hardware, funds, facilities, access - a network path from the source host to the victim and vice versa, network access from an ISP)

Social-Political Component
- Describes the needs and intent of the adversary
	- ie financial gain - gaining acceptance in the hacker community, hacktivism, or espionage

Technology Component
- Highlights the relationship between the core features - capability and infrastructure
- Capability and infrastructure describe how the adversary operates and communicates
- A scenario:
	- A watering-hole attack which is a methodology where the adversary compromises legitimate website that they believe their targeted victims will visit
- 