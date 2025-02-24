https://tryhackme.com/room/phishingemails4gkxh

- Email Security
	- SPF, DKIM, DMARC
- SPAM Filters
	- Flags or blocks incoming emails based on reputation
- Email Labels
	- Alert users that an incoming email is from an outside source
- Email Address/Domain/URL Blocking
	- Based on reputation or explicit deny list
- Attachment Blocking
	- Based on the extension of the document
- Attachment Sandboxing
	- Denoting email attachments in a sandbox environment to detect malicious activity)
- Security Awareness Training
	- Internal phishing campaigns

Phishing for Information
- An attempt to trick targets into divulging information, sub-techniques:
	- Spearphishing Service
	- Spearphishing Attachment
	- Spearphishing Link
	- Spearphishing Voice

Mitigations
- Software Configuration
	- Anti-spoofing and email authentication mechanisms to filter messages on validity checks of the sender domain (using SPF) and integrity of messages (using DKIM). 
	- Enabling these mechanisms within an organisation (through policies such as DMARC) may enable recipients (intra and cross domain) to perform similar message filtering and validation.
- User Training
	- Train users to be able to better identify social engineering techniques and spearphishing attempts

Sender Policy Framework (SPF)
https://dmarcian.com/create-spf-record/
- SPF is used to authenticate the sender of an email
- With a SPF record in place, ISPs can verify that a mail server is authorised to send email for a specific domain
- A SPF record is a DNS TXT record containing a list of the IP addresses that are allowed to send email on behalf of your domain
- ![](https://assets.tryhackme.com/additional/phishing4/dmarcian-spf.png)
- An SPF record can look like this:
	- `v=spf1 ip4:127.0.0.1 include:_spf.google.com -all`
	- `v=spf1` - the start of the SPF record
	- `ip4:127.0.0.1` - Specifies which IP can send mail
	- `include:_spf.google.com` - Specifies which domain can send mail
	- `-all` - non-authorised emails will be rejected

DKIM (DomainKeys Identified Mail)
https://dmarcian.com/dkim-selectors/
- DKIM is used for the authentication of an email that's being sent
- Like SPF, DKIM is an open standard for email authentication that is used for DMARC alignment. 
- A DKIM record exists in the DNS, but it is a bit more complicated than SPF
- DKIM's advantage is that it can survive forwarding, which makes it superior to SPF and a foundation for securing emails
- A DKIM record can look like this:
	- `v=DKIM1; k=rsa; p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAxTQIC7vZAHHZ7WVv/5x/qH1RAgMQI+y6Xtsn73rWOgeBQjHKbmIEIlgrebyWWFCXjmzIP0NYJrGehenmPWK5bF/TRDstbM8uVQCUWpoRAHzuhIxPSYW6k/w2+HdCECF2gnGmmw1cT6nHjfCyKGsM0On0HDvxP8I5YQIIlzNigP32n1hVnQP+UuInj0wLIdOBIWkHdnFewzGK2+qjF2wmEjx+vqHDnxdUTay5DfTGaqgA9AKjgXNjLEbKlEWvy0tj7UzQRHd24a5+2x/R4Pc7PF/y6OxAwYBZnEPO0sJwio4uqL9CYZcvaHGCLOIMwQmNTPMKGC9nt3PSjujfHUBX3wIDAQAB`; `
- The key is a public key that will be matched to the corresponding private key (which is created during the DKIM setup process)
- Essentially a receiver can confirm whether an email that is inbound has been sent from the domain that it says that it is coming from - through the use of the domain's public key

DMARC (Domain-Based Message Authentication, Reporting, and Conformance)
- https://dmarcian.com/what-is-a-dmarc-record/
- https://dmarcian.com/getting-started-with-dmarc/
- DMARC is an open-source standard and uses a concept called alignment to tie the result of two other open source standards, SPF and DKIM, to the content of an email
- Putting a DMARC record into place for your domain will give you feedback that will allow you to troubleshoot your SPF and DKIM configurations if needed
- A DMARC record can look like this:
	- `v=DMARC1; p=quarantine; rua=mailto:postmaster@website.com`
	- `p=quarantine` - If a check fails, then an email will be sent to the SPAM folder (DMARC Policy)
	- `rua=mailto:postmaster@website.com Aggregate reports will be sent to this email address
- A DMARC is a text entry within the DNS that tells the world your emails domain's policy when it comes to checking to see if your SPF and/or DKIM has passed or failed
- Receiving servers send XML reports back to the reporting email address that is listed in the DMARC record
	- These reports provide insight on how your email is moving through the ecosystem and allow you to identify everything that is using your email domain
- Domain Health Checker from dmarcian:
	- https://dmarcian.com/domain-checker/

S/MIME (Secure/Multipurpose Internet Mail Extensions)
- https://learn.microsoft.com/en-us/exchange/security-and-compliance/smime-exo/smime-exo
- S/MIME is a widely accepted protocol for sending digitally signed and encrypted messages
- Digital Signatures - verify the sender of an email message
- Encryption
- Providing:
	- Authentication
	- Nonrepudiation
	- Data integrity
- A digital certificate will be needed - within which there will be a public key
	- This digital certificate can then be signed with the respective private key associated with the public key
	- Recipients can then decrypt the message with the public key 
	- In replying to the original email, the recipient will send their own digital certificate
	- Both ends will then have each others digital certificate in moving forward

- SMTP Status Codes
	- https://en.wikipedia.org/wiki/List_of_SMTP_server_return_codes