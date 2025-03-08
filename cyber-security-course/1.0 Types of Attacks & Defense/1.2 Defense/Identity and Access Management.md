Identification
Authentication
Authorisation
Accounting
	AAA

Identification
- Claiming an identity
Authentication
- Proving that identity
- MFA
	- Using multiple ways/methods/factors to authenticate an account or login
	- Something you know
	- Something you have 
	- Something you are
- Attributes
	- Breaking down the factors
	- Something that you can do 
		- ie signature
	- Something you exhibit
		- ie typing speed
	- Someone you know
	- Somewhere you are
Authorisation
- Permitting specific actions or access once a User has been authenticated
- Determines resource permissions
- Resources
	- Files on a server
	- Rows in a database
	- A web-application
Accounting / Auditing
	Audit the activity of logins/sessions (what happened? When/Where/With?etc)
- Tied to authentication in that a user's activity is audited based on what a user has permission to do on a system
- Ensure each user has their own account (SEPARATE ACCOUNTS are key)
	- Resource access
	- Failed logon attempts
	- Changes to files/database records
- Logging

IAM - Identity and Access Management

- Authentication Methods
	- Usernames/Passwords
	- Password Managers
	- OTP
		- One-Time Password
	- TOTPs
		- Time-based OTPs
	- HOTP - HMAC-based OTP 
	- HMAC
		- Hash-based Message Authentication code
		- A specific type of message authentication code involving a cryptographic hash function and a secret cryptographic key
	- Certificate-Based Authentication
		- PKI certificates are issued by a CA to an individual entity
		- Device, VPN, app access
	- Can be stored on a smart card
			- Called a PIV
				- Personal Identity Verification
	- CACs
			- Common-Access Cards
	- SSH Public Key Authentication
	- Biometrics
		- Fingerprint scans
		- Retina scans
		- Iris scans
		- Facial recognition
		- Voice
		- Vein analysis
		- Gait analysis
			- How you move, walk
		- Efficacy Rates
			- False acceptance rate
			- False rejection rate
			- Crossover error rate
- Access Control Schemes
	- Credential Policies
		- Defines who gets access to what
			- Employees
			- Contractors
			- Devices
			- Service Accounts
				- Can be known as Managed Identities on platforms like Azure
			- Administrator/Root Accounts
				- PAM accounts (Privileged Access Management)
	- Attribute-Based Access Control
		- ABAC
		- Defining user or device attributes that can determine access to resources
			- Example DOB for a person wanting to get a drivers license
			- The version of a software before allowing or determining its access
	- Role-Based Access Control
		- RBAC
			- Defining roles which have access to resources
	- Rule-Based Access Control
		- Uses conditional access policies
		- In example, using MFA on an Android device, from New Zealand
		- Rules are applied
	- Mandatory Access Control (MAC)
		- Assigning labels or identifiers to reources
			- files, network ports, databases and the such
		- Permissions are determined by resource labels and security clearance
	- Discretionary Access Control
		- DAC
			- The custodian of the resource sets the permissions at their discretion
	- Physical Access Control
		- Physical access vestibules
			- Fob key, locks on doors, gates, and so on
		- Limited physical access to buildings

- Account Management
	- Unique account per user
	- Organising users into groups
	- Principle of least privilege
	- User account auditing
	- Disabling accounts upon employee/user exits
		- Processing accordingly
	- Rights/privileges 
	- Account types
		- User, device, service
		- Admin/root
		- Privileged
		- Guest
	- Account Policies
		- Employee Onboarding
		- Password Policies
			- Complexity
			- Password History
			- Reuse
		- Account Lockouts
		- Time-based Policies
			- Enforce login/logout times
		- Geolocation Policies
			- Where is the login coming from
			- Where is the device located
		- Geofencing
			- User geolocation determines resource access
		- Geotagging
			- Adding location metadata to files and social media posts
		- Impossible travel time
		- Risky login
			- Time of login (abnormal time?)
		- Baselining User Activities
			- The common norm
	- Different types of user accounts can have different account policies applied
	- Each user should have their own account with only the permissions required to perform job tasks
	- Password policies control password complexity, history, and expiration
	- Assigning permissions to groups is scalable
	- Geofencing uses the device's physical location to determine resource access

- Network Authentication
	- PAP - Password Authentication Password
		- Don't use this, it's legacy
		- It sends cleartext transmissions of passwords
	- MS-CHAPv2
		- Microsoft Challenge Authentication Protocol
	- NTLM
		- New Technology LAN Manager
		- NTLMv2 uses salting
	- Kerberos
		- MS AD authentication
		- KDC
			- Kerberos Key Distribution Centre
		- AS
			- Authentication Service
		- TGS
			- Ticket Granting Service
		- TGT
			- Ticket Granting Ticket
	- Kerberos is used for Active Directory
	- NTLMv2 is used for Local Workgroup Computers
	- Extensible Authentication Protocol (EAP)
		- used in Windows environments
		- used in VPN environments
		- Using PKI certificates, smart cards
		- EAP uses TLS as a transport mechanism

IAAA
- Identification
	- The process of verifying who the user is 
		- Starts with the user claiming a specific identity - can be a unique identifier like an email address, a username or an ID number
- Authentication
	- The process of ensuring that the user is who they are claiming to be
		- Confirming the claimed identity
		- Providing the correct password for example
		- MFA and so on (biometrics!)
- Authorisation
	- Determines what the User is allowed to access
		- This process is typically carried out by assigning roles and permissions based on the user's job function or level of clearance
		- The risk of unauthorised access or data breaches is reduced by restricting access to only the resources necessary for the user to perform their duties
- Accountability
	- Tracks user activity to ensure they are responsible for their actions
		- After a user is granted access to a system - it would be essential to have mechanisms that hold everyone accountable for their actions
		- Achieved by logging all user activity and storing it in a centralised location
		- In the event of a security incident, this information can be used to identify the source of the problem and take appropriate action

- IAAA helps to prevent unauthorised access, data breaches and other security incidents 

Logging
- Log forwarding is the process of sending log data from one system to another
	- Aggregates log data from multiple sources into a central location for more accessible analysis and management
	- Can be used to send log data to a cloud-based service for storage and analysis
	- Centralising log data - organisation can efficiently analyse and correlate log events from different systems to identify potential security threats
		- Such as via the use of a SIEM for example
- To ensure that accountability is kept for any critical component of the infrastructure
	- The logs should be performed properly and kept securely
	- Tamper-proof
- Good practice to set up a separate logging server with one task - receiving and storing logs, securely

Identity Management (IdM)
- Includes the necessary policies and technologies for identification, authentication and authorisation
- IdM aims to ensure that authorised people have access to the assets and resources needed for their work while unauthorised people are denied access. 
- Identity Management
	- By implementing effective IdM strategies - organisations can ensure that their users are authenticated and authorised to securely access the resources they need
- Some sources may refer to Identity Management and Identity and Access Management interchangeably
- Other sources may consider Identity Management to be more focused on the security issues related to user identity, such as authentication and permissions
	- They state that IdM is concerned with managing the attributes and permissions of users, devices and groups
	- While IAM is more concerned with evaluating the attributes and permissions and granting or denying access according to company policy
- IdM
	- An essential component of cybersecurity that refers to the process of managing and controlling digital identities
	- It involves the management of user identities, their authentication, authorisation, and access control
	- The main goal of IdM is to ensure that only authorised individuals have access to specific resources and information
	- IdM systems use a centralised database to store user identities and access rights, they also provide functionalities to manage and monitor user access to resources
	- IdM systems generally include features such as user provisioning, authentication and authorisation
	- User provisioning refers to the process of creating and managing user accounts, while authentication and authorisation refer to verifying the identity of a user and granting access to specific resources
- IAM
	- More comprehensive of a concept from IdM
	- Encompasses all the processes and technologies to manage and secure digital identities and access rights
	- IAM systems include a variety of functions, such as 
		- user provisioning
		- access control
		- identity governance; and
		- compliance management
	- IAM systems ensure that only authorised users have access to specific resources and data and that their access is monitored and controlled
	- IAM systems provide a more comprehensive solution to manage and secure access to resources in an organisation
	- They integrate with multiple systems and applications, providing a centralised view of user identities and access rights
	- IAM systems use various technologies to manage access, including role-based access control, MFA, and SSO 
	- IAM systems help organisation comply with regulatory requirements such as HIPAA, GDPR, PCI DSS and the like
	- They provide functionalities to manage the lifecycle of user identities, including onboarding, offboarding and access revocation
	- In addition, IAM systems allow organisations to track and audit user activity, which helps to prevent security breaches and ensure compliance with industry regulations

- Access Control Models
	- DAC - Discretionary Access Control
	- RBAC - Role-Based Access Control
	- MAC - Mandatory Access Control
- Discretionary Access Control (DAC)
	- The resource owner will explicitly add users with appropriate permissions
- Role-Based Access Control (RBAC)
	- Each user has one or more roles or functional positions - they are authorised to access different resources based on their roles
- Mandatory Access Control (MAC)
	- An OS using MAC will prioritise security and significantly limit users' abilities. 
	- These systems are used for specific purposes or to handle highly classified data
	- Users do not need to carry out tasks beyond the strictly necessary
		- Such as installing new software or changing file permissions
	- AppArmor gives the ability to have MAC on a Linux distro
	- SELinux project provides a flexible MAC for Linux systems

Single Sign-on
- Allows users to use one password to login to multiple systems
- As opposed to having to remember different usernames and passwords for each system that they would otherwise log into
- Makes work scenarios more efficient and user-friendly for end-users

CIA
IAAA - Identification, Authentication, Authorisation, Access Control, Accountability, and Logging (along with others)

