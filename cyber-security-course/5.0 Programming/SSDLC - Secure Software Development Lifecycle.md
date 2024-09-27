
- Aims to introduce security at every stage of the SDLC
- Research at IBM in their Systems and Sciences Institute discovered that it would cost six times more to fix a bug during the implementation phase of the SDLC - than one that was identified as early as during the design phase. 
	- It also had identified that it would cost 15 times more if the flaws were found during testing, and up to 100 times more if found during the maintenance and operation phases. 
- Faster development
- Reduction of costs
- Assists in discovering and reducing the vulnerability count early 
	- Thus reducing business risk significantly
- Examples:
	- Architecture analysis during design
	- Code review and scanners during development
	- Conducting security assessments (pentests) before deployment

- Security is a constant concern, which can improve quality and security of the software constantly 
- Boosting the education and awareness of security allows all stakeholders to know each phase's security recommendations and requirements
- Flaws would be detected early - before deployment.
	- Reducing the risk of getting hacked, or disruptions
- Costs would be reduced, speed would increase - due to detecting vulnerabilities and the resolution to said vulnerabilities, early.
- Business risk, reputation damage, and fines that could lead to economic disaster for a company would be prevented

- Implementing SSDLC
	- Gap Analysis
		- Determines what activities and policies exist in the organisation and how effective they are
			- Ensuring policies are place (what the system/people do)
			- Ensuring security procedures are in place (how those policies are executed)
	- Software Security Initiatives (SSI)
		- Establishing achievable and realistic goals which are defined metrics for success
			- Like a secure coding standard, playbooks for handling data, and so on
		- Tracked by using project management tools
	- Formalise Processes
		- For the security activities within the Software Security Initiative(s)
		- After a program or standard has started or has been announced - it would be essential to spend a period of operations to help engineers get familiar with it and getting feedback from them before enforcing it.
		- When carrying out a gap analysis - every policy should have defined procedures to make them effective
	- Security Training
		- For engineers and the related tools they would use
		- Ensuring that people are aware of new processes and the tools that will come with them
		- Investing into training early, before establishing and onboarding the new tool/process

- SSDLC Processes
  Involves integrating and prioritising security related processes like security testing and other activities into an existing SDLC phase/process ONCE the related security posture is understood
	  Examples: 
		  - Writing security requirements alongside functional requirements
		  - Performing an architecture risk analysis during the design phase
	- Risk Assessment (Planning and Requirements Definition phases)
		- Identifying security considerations that promote a security by design approach when functional requirements are gathered in the planning and requirements phases
			- Example: A user requests a blog entry from a site, they should not be able to edit the blog or remove unnecessary input fields
	- Threat Modelling (Design and Prototyping phases)
		- Identifying potential threats when there is a lack of appropriate safeguards. 
		- Effective when following a risk assessment and during the design stage of the SDLC
		- Focuses on what should NOT happen
			- Where as the Design phase would normally only outline how the software application will behave and interact
	- Code Scanning and Review (Software Development and Testing phases)
		- Code reviews can either be manual or an automated process
		- Code scanning or automated code reviews can leverage Static and Dynamic Security testing technologies
		  Critical in the Development Stage as the code is being written
	- Security Configuration (Deployment phase)
	- Security Assessments - ie Penetration Testing and Vulnerability Assessments (Operations and Maintenance phase(s))
		- Form of automated testing that can identify critical paths of an application that may lead to exploitation of a vulnerability
			- Hypothetical as the assessment doesn't carry simulations of those attacks
		- Pentesting, however, identifies these flaws and attempts to exploit them to demonstrate validity
		- These activities are carried out after a prototype of an application has been created and in the Operations and Maintenance phases

- Risk Assessment
	- 