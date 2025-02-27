https://tryhackme.com/room/securityengineerintro
- Owns the overall security of an organisation
	- Securing an organisation's digital assets
- Ensures that the organisation's cyber security risk is minimised, at all times
- Forms strategies and creates systems that minimise the risk posed by cyber security threats to an organisation 
- Conducts tests to ensure the robustness of the cyber security posture of an organisation, identifies weak points and prepares for mitigations
- Develops and implements secure network solutions
- Architects and engineers trustworthy, reliable, and secure systems
- Collaborates and coordinates with other teams to establish security protocols across the organisation

Asset Management / Asset Inventory / Asset Register
- Keeping an up-to-date register of all digital assets
- Name, type, IP addresses, physical locations, place in the network, applications running on a host, access permissions, asset owners, etc

Security Policies
- Robust security policies should be kept to maintain a sound security posture
- The security engineer will assist in the creation of such policies based on established security principles (CIA, DAD - Disclosure, Alteration, Destruction/Denial), Defence-in Depth, Zero Trust, Trust But Verify, Threats/Risks etc). 
- These policies are then implemented organisation-wide, and the security engineer ensures that the implementation follows the letter and spirit of the policies. 

Secure by Design
- The security engineer ensures that the organisation is secure by design.
- Will understand IT Governance, and that the security posture receives the most ROI if it follows a secure-by-design philosophy. 
- The sec engineer will take steps to implement a Secure Network Architecture - keeping all systems hardened, SDLC's following the SSDLC. 

Security Assessment and Assurance
- To mitigate risks from a continuously evolving threat landscape - a security engineer will plan to conduct regular security assessments, audits, red-teaming and purple-teaming exercises to continuously improve the security posture

Continuous Improvement
- A company's security is not a one-off job but rather a continuous effort
- Same thing with the Security Engineers roles/jobs that is carried out post the design and implementation of security policies
- Ensuring Awareness
	- Human's tend to be the weakest link in an organisation's security
	- Running awareness sessions targeting social engineering attacks (and similar) can assist in ensuring that human's don't make mistakes that can compromise the organisation
		- These sessions/programs are also organised for specific teams to ensure they follow security principles related to their area of expertise - like secure software development or secure network architecture

Managing Risks
- Risk assessments where the identification of security risks is made, determining those risks' likelihood and impact on the business and finding solutions to minimise those risks.
- Eliminating all risks might not be possible when running business operations - sometimes, a decision has to be made to accept a risk and move on
- Accepting or mitigating risks is often a business decision 
	- The security engineer acts as a trusted advisor to the management team that helps them make these decisions by providing subject matter expertise
	- Taking an example of of an organisation that uses a specific database software for its supply chain that is running on an outdated and vulnerable version of Linux
		- The DB is crucial to the business
		- Updating the underlying Linux distribution to the latest and secure version without impacting operations may require significant effort 
			- It would require engagement with the DB vendor, who may or may not have tested its software on the latest version of the related Linux distro
		- Making any permanent production changes without testing will more than likely lead to issues arising 
		- Assessing that the vulnerable Linux distro poses a security risk as well
		- A security engineer may suggest to mitigate the risk by hardening the OS through controls and adding a reverse proxy in front of the system to avoid exposing it to the Internet
		- This doesn't eliminate the risk, but it will significantly reduce the risk without affecting the company's operations

Change Management
- Organisations evolve, which results in their security posture having to change as that evolution progresses
- To ensure a robust security posture, the security engineer keeps track of changes in the organisation's digital assets that can affect the security posture and takes measures to improve the security posture with the organisation's evolution
- Say for an example an upgrade/update to an e-ecommerce module for the company's website - to better cater for its corporate customers
	- The new module would need a:
		- Risk assessment
		- Penetration test(ing)
		- Vulnerability assessment
		before integrating with the production website
	- The security engineer would need to ensure that these requirements are fulfilled and that the integration will not introduce security vulnerabilities 
	- Furthermore, it will also be ensured that the new module follows all the security policies and guidelines laid out by the organisation

Vulnerability Management
- The threat landscape, too, is constantly evolving
- New software versions are released, new vulnerabilities are found in new and older versions
- The security engineer's role will often include monitoring for these vulnerabilities across the organisation and planning to patch or minimise their potential risks
- Vulnerabilities are generally patched according to severity (vulnerability management)

Compliance and Audits
- A significant part of a security engineer's duties includes ensuring compliance with regulatory and organisation requirements
- PCI-DSS, HIPAA, SOC2, ISO27001, NIST-800-53 and more
- The sec engineer will work closely with both internal and external auditors to detect any non-compliance issues and effectively address them
- Additionally, they are responsible for upholding the organisation's security certifications as needed

Additional Roles and Responsibilities
- Managing Security Tooling
	- The configuration or fine-tuning of security tools like SIEMs, Firewalls, WAFs, EDRs, and the like will be required. 
	- In some cases, depending on the size of the organisation, this may be the primary responsibility of the engineer
	- The Security Engineer may also be making decisions or providing input to decision-makers about tools to procure, based on the organisation's requirements and the engineer's assessment of competitive tools
- Tabletop Exercises
	- These exercises are often conducted to gauge the operational readiness of an organisation from a security perspective
	- Certain scenarios can be identified to be exercises, and security team members must explain their respective roles in the scenario's under discussion
	- For example - a scenario might include the compromise of an endpoint through a phishing email 
		- All the team members will then explain their respective steps per the organisation's playbooks
		- The security engineer will also sometimes be required to conduct these exercises
- Disaster Recovery and Crisis Management
	- A robust security posture requires an organisation to plan for untoward incidents, disasters or crises. 
	- The top priority of the exec team is to maintain business continuity
	- A security engineer might be involved in DR, BC, and crisis management planning as part of the different compliance frameworks and the organisation's internal policies
	- The role of a security engineer in these areas might differ depending on the organisation

Security engineers must consider various aspects of running a business apart from keeping it secure. These may include business operations, cost, ease of implementation, ease of use, and more. 
"Although the most secure system is the one that is shut off and disconnected from power, such a system doesn't achieve any business objectives."
A security engineer must consider these business objectives and security when decision-making.

Conclusion - a Security Engineer will:
- Own the responsibility of an organisation's cyber security
- Ensure that systems and infrastructure of the organisation are built securely
- Assists in maintaining this security posture through continuous improvement and changes in the organisation's digital assets
- Takes on additional roles and responsibilities to help other teams achieve the collective goal of a secure organisation