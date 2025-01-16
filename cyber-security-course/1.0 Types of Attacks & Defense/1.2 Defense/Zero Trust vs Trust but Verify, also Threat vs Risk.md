https://tryhackme.com/r/room/securityprinciples

Two security principles:
- Trust but Verify
- Zero Trust

Trust but Verify
- Teaches that we should always verify even when we trust an entity and its behaviour
	- Entity could be a user or an entire system, a device
- Usually requires setting up appropriate logging mechanisms
- Verifying indicates going through logs to ensure that everything is 'normal'
- Requires automated security mechanisms
	- Proxy
	- Intrusion Detection Systems
	- Intrusion Prevention Systems

Zero Trust
- Treats trust as a vulnerability
- Caters to insider-related threats
- Zero trust tries to eliminate trust
- "Never trust, always verify"
- Does not grant trust based on its location or ownership
- If any breach occurs, the damage would be more contained if this architecture is in place
- Microsegmentation is one of the implementations used for Zero Trust
	- Refers to the design where a network segment can be as small as a single host
	- Communication between segments require authentication, ACL checks, and other security requirements
- There is a limit to how much we can apply zero trust without negatively impacting a business
	- This doesn't mean, however, that we should not apply it as long as it is feasible

Threat vs Risk
- Vulnerability
	- Susceptible to attack or damage
	- Information security, a vulnerability is a weakness
- Threat
	- Potential danger associated with this weakness or vulnerability
- Risk
	- Concerned with the likelihood of a threat actor exploiting a vulnerability and the consequent impact on the business

