https://learn.microsoft.com/en-us/training/modules/describe-cloud-compute/1-introduction-microsoft-azure-fundamentals
- MS Azure is a cloud computing platform with an expanding set of services that helps to build solutions to meet business goals/objectives
- Has simple web services for hosting a businesses presence in the cloud
- Supports running fully virtualized computers managing custom software solutions
- Provides cloud-based services like remote storage, database hosting, centralized account management
- AI and IoT focused services provided

Introduction to Cloud Computing
- Define cloud computing
- Describe the shared responsibility model
- Define cloud models, including public, private and hybrid
- Identify appropriate use cases for each cloud model
- Describe the consumption-based model
- Compare cloud pricing models

What is Cloud Computing
- Cloud computing is the delivery of computing services over the Internet.
- Computing services include common IT infrastructure such as VMs, storage, DBs, and networking
- Cloud services can also expand the traditional IT offerings to include things like IoT, ML (Machine Learning) and Artificial Intelligence
- Since Cloud Computing uses the Internet to deliver these services, it doesn't have to be constrained by physical infrastructure the same way that a traditional datacentre is
- Meaning you can increase IT infrastructure rapidly - you don't have to wait to build a new datacenter, and you can use the cloud to rapidly expand a company's IT footprint.
- Basic Services
	- Compute Power
		- How much processing a computer can do (RAM, CPU cores)
	- Storage
		- Volume of data that you can store on the computer
		- Drive space
- Backups, OS versions are up to date
- As a business grows, and computing needs change, you can change what you need as needed - scalable

Describe the Shared Responsibility Model
- Consider a traditional datacentre
	- The datacentre is responsible here for maintaining physical space, ensuring security, maintaining or replacing servers if anything happens
	- The IT department is responsible for maintaining all the infrastructure and software needed to keep the datacentre up and running
	- They're also likely to be responsible for keeping all the systems patched and on the correct version
- The shared responsibility model 
	- These responsibilities get shared between the cloud provider and the consumer
	- Physical security, power, cooling and network connectivity are the responsibility of the cloud provider
	- The consumer isn't collocated with the datacentre
		- So it doesn't make sense for the consumer to have any of those responsibilities
- At the same time - the consumer is responsible for the data and information stored in the cloud
	- You wouldn't want the cloud provider to be able to read your information or have access to your data!
	- The consumer is also responsible for access security, meaning that you only give access to data/systems to those who need it
- For some things, the responsibility depends on the situation
	- If you're using a cloud SQL database, the cloud provider would be responsible for maintaining the actual database
	- The consumer will be responsible for the data that gets ingested into the database
	- If a VM is deployed and a SQL database is installed on it, then the installer (or whoever is responsible) will be responsible for database patches and updates, as well as maintaining the data and information stored in the database
- With an on-prem datacentre
	- You're responsible for everything.
- With cloud computing
	- These responsibilities shift
- The shared responsibility model is heavily tied into the cloud service types
	- IaaS (Infrastructure As A Service)
		- Places the most responsibility on the consumer
		- With the cloud provider being responsible for the basics of physical security, power, and connectivity
	- PaaS (Platform As A Service)
		- Middle ground of responsibility
		- Evenly distributes responsibility with the cloud provider and the consumer
	- SaaS (Software As A Service)
		- Most of the responsibility is placed with the Cloud Provider
	![](https://learn.microsoft.com/en-us/training/wwl-azure/describe-cloud-compute/media/shared-responsibility-b3829bfe.svg)

- When using a cloud provider - the consumer will always be responsible for:
	- The information and data stored in the cloud
	- Devices that are allowed to connect to the cloud (cellphones, computers, and so on)
	- The accounts and identities of the people, services, and devices within the organisation
- The cloud provider is always responsible for:
	- The physical datacentre
	- The physical network
	- The physical hosts
- Service Model will determine responsibility for things like: 
	- Operating Systems
	- Network controls
	- Applications
	- Identity and infrastructure

Define Cloud Models
- Cloud models define the deployment type of cloud resources
- Private Cloud
	- The natural evolution from a corporate datacentre
	- It's a cloud (delivering IT Services over the Internet) that's used by a single entity
	- Private cloud provides much greater control for the company and its IT department
	- It also comes with a greater cost and fewer benefits of a public cloud deployment
	- A private cloud may be hosted from your on site datacentre
	- It may also be hosted in a dedicated datacentre offsite
	- Potentially even by as third party that has dedicated that datacentre to your company
	- Organisations have complete control over resources and security
	- Data is not collocated with other organisations data
	- Hardware must be purchased for startup and maintenance
	- Organisations are responsible for hardware maintenance and updates
- Public Cloud
	- A public cloud is built, controlled and maintained by a third-party cloud provider
	- With a public cloud, anyone that wants to purchase cloud services can access and use resources
	- The general public availability is a key difference between public and private clouds
	- No capital expenditures to scale up
	- Applications can be quickly provisioned and deprovisioned
	- Organisations pay only for what they use
	- Organisations don't have complete control over resources and security
- Hybrid Cloud
	- Hybrid cloud is a computing environment that uses both public and private clouds in an inter-connected environment
	- A hybrid cloud environment can be used to allow a private cloud to surge for increased, temporary demand by deploying public cloud resources. 
	- Hybrid cloud can be used to provide an extra layer of security
	- For example - users can flexibly choose which services to keep in public cloud and which to deploy to their private cloud infrastructure
	- Provides the most flexibility
	- Organisations can determine where to run their applications
	- Organisations control security, compliance and legal requirements
- Multi-Cloud
	- Multiple public cloud providers are used
	- Different features perhaps from different cloud providers
	- Maybe the journey started with one cloud provider and the company is in the process of migrating to a different provider
	- Multi-cloud environments involve dealing with two ore more public cloud providers and managing resources and security in both environments
- Azure Arc
	- Azure Arc is a set of technologies that helps manage a cloud environment
	- Arc can help manage the cloud environment, whether it's public cloud solely on Azure, a private cloud in a datacentre, or a hybrid configuration - even a multi-cloud environment running on multiple cloud providers at once
- Azure VMware Solution
	- If there is a VMware solution that is sitting in a private cloud environment and the decision to migrate to a public or hybrid-cloud solution is made - Azure's VMware Solution lets a business run those VMware workloads in Azure with seamless integration and scalability

Describe the Consumption-based Model
- When comparing IT infrastructure models, there are two types of expenses to consider
	- CapEx
		- Capital Expenditure
		- A one-time, up-front expense to purchase or secure tangible resources
		- A new building, repaving a parking lot, building a datacentre, or buying a company vehicle are example of CapEx
	- OpEx
		- Spending money on services or products over time
		- Renting a convention centre, leasing a vehicle, signing up for cloud services are examples of OpEx
- Cloud computing falls under OpEx as cloud cloud services run on a consumption-based model
- With cloud computing, you don't pay for the physical infrastructure, the electricity, the security, or anything else associated with maintaining a datacentre
	- Instead, you pay for the IT resources you use
	- You don't pay for IT resources that aren't used in a month
- Benefits
	- No upfront costs
	- No need to purchase and manage costly infrastructure that users might not use to its fullest potential
	- The ability to pay for more resources when they're needed
	- The ability to stop paying for resources that are no longer needed
- With a traditional datacentre, you try to estimate future resource needs
- If you overestimate then you spend more on your datacentre than you need to and potentially waste money
- If you underestimate, the datacentre will quickly reach capacity and your applications and services may suffer from decreased performance
- Fixing an under-provisioned datacentre can take a long time
	- You may need to order, receive, and install more hardware
	- You'll also need to add power, cooling and networking for the extra hardware
- In a cloud-based model
	- You don't have to worry about getting the resources just right
	- If you need more VMs, you add more
	- If the demand drops and you don't need as many VMs, you remove them as required
	- You're only paying for the VMs that you use, not the extra capacity that the cloud provider has on hand.

Compare Cloud Pricing Models
- Cloud computing is the delivery of computing services over the Internet by using a pay-as-you-go pricing model
- You typically only pay for the cloud services you use, which helps to:
	- Plan and manage operating costs
	- Run infrastructure more efficiently
	- Scale as the business changes
- Cloud computing is a way to rent compute power from someone else's datacentre. 
- You can treat cloud resources like you would resources in your own datacentre
- However, unlike your own datacentre, when you're finished using cloud resources, you give them back (lol)
- Instead of maintaining CPUs and storage in a datacentre, you rent them for the time that you need them.

https://learn.microsoft.com/en-us/training/modules/describe-benefits-use-cloud-services/1-introduction
- Describe the benefits of high availability and scalability in the cloud
- Describe the benefits of reliability and predictability in the cloud
- Describe the benefits of security and governance in the cloud
- Describe the benefits of manageability in the cloud

Describe the Benefits of High Availability and Scalability in the Cloud
- When building or deploying a cloud application - two of the biggest considerations are uptime (availability) and the ability to handle demand (scalability)

High Availability
- When deploying an application, service, or any IT resources - it's important that the resources are available when needed
- High availability focuses on ensuring maximum availability, regardless of disruptions or events that may occur
- When you're architecting your solution, you'll need to account for service availability guarantees
- Azure is a highly available cloud environment with uptime guarantees depending on the service
- These guarantees are a part of the SLAs

Scalability
- Another benefit of cloud computing is the scalability of cloud resources
- Scalability refers to the ability to adjust resources to meet demand
- If you suddenly experience peak traffic and systems are overwhelmed, the ability to scale means you can add more resources to better handle the increased demand
- Another benefit is that you aren't overpaying for services
- Because the cloud is a consumption-based model, only what is used is paid for
- Scaling generally comes in two varieties
	- Vertical Scaling
		- Focused on increasing or decreasing the capabilities of resources
		- If one was developing an app and more processing power was needed, you could vertically scale up to add more CPUs and/or RAM to the VM
		- If you realised that you had over-specified your requirements, then you could vertically scale down by lowering those resources
	- Horizontal Scaling
		- Adding or subtracting the number of resources
		- If you experienced a sudden steep jump in demand, your deployed resources could be scaled out (either automatically, or manually)
			- Ie - you could add additional VMs or Containers, scaling out
		- In the same manner, if there was a drop in demand - deployed resources could be scaled in (automatically or manually). 

Benefits of Reliability and Predictability in the Cloud
- Reliability and predictability are two crucial cloud benefits that help you develop solutions with confidence
- Reliability
	- The ability of a system to recover from failures and continue to function
	- One of the pillars of the Microsoft Azure Well-Architected Framework
	- Due to the decentralised design of the cloud allows it to naturally support a reliable and resilient infrastructure
	- With a decentralized design, the cloud enables you to have resources deployed in regions around the world
	- With a global scale, even if one region has a catastrophic event, there are other regions that are still up and running
	- You can design your applications to automatically take advantage of this increased reliability
	- In some cases - your cloud environment itself will automatically shift to a different region for you with no needed action on the IT admins part
- Predictability
	- Predictability in the cloud lets you move forward with confidence
	- Predictability can be focused on performance predictability or cost predictability
	- Both are heavily influenced by the MS Azure Well-Architected Framework
	- Deploy a solution that is built around this framework and you have a solution whose cost and performance are predictable
	- Performance Predictability
		- Focuses on predicting the resources needed to deliver a positive experience for your customers
		- Autoscaling, load balancing, and high availability are just some of the cloud concepts that support performance predictability
		- If the company needs more resources suddenly - then autoscaling can deploy additional resources to meet the sudden demand - then scale back when the demand drops
		- Or if the traffic is heavily focused on one area, then load-balancing will help redirect some of the overload to less stressed areas
	- Cost Predictability
		- Focused on predicting or forecasting the cost of the cloud spend
		- With the cloud you can track your resource use in real time, monitor resources to ensure that you're using them in the most efficient way, and apply data analytics to find patterns and trends that help better plan resource deployments
		- By operating in the cloud, and using cloud analytics and information, you can predict future costs an adjust your resources as needed
		- You can use tools like the TCO (Total Cost of Ownership) or Pricing Calculator to get an estimate of potential cloud spend

Describe the Benefits of Security and Governance in the Cloud
- Whether IaaS or SaaS is being deployed, cloud features will support compliance and governance.
- Things like set templates help ensure that all your deployed resources meet corporate standards and government regulatory requirements. 
- Deployed resources can be updated to new standards as standards change
- Cloud-based auditing helps flag any resource that's out of compliance with your corporate standards and provides mitigation strategies
- Depending on the operating model, software patches and updates may also automatically be applied - which helps with both governance and security
- A cloud solution can be found that matches a company's security requirements
- If you want maximum control of security, IaaS provides you with physical resources but lets you manage the OSes and installed software, including patches and maintenance. 
- If you want patches and maintenance to be taken care of automatically, then PaaS or SaaS service deployments may be the best cloud strategies for you
- And because the cloud is intended as an over-the-Internet delivery of IT resources, cloud providers are typically well suited to handle things like DDoS attacks, making your network even more robust and secure.
- By establishing a good governance footprint early, you can keep your cloud footprint updated, secure, and well managed.

Describe the Benefits of Manageability in the Cloud
- Two types of manageability for cloud computing - both are excellent benefits
- Management of the Cloud
	- Automatically scale resource deployment based on need
	- Deploy resources based on a preconfigured template, removing the need for manual configuration
	- Monitor the health of resources and automatically replace failing resources
	- Receive automatic alerts based on configured metrics, so you're aware of performance in real time
- Management in the Cloud
	- Through a web portal
	- Using a CLI
	- Using APIs
	- Using PowerShell

https://learn.microsoft.com/en-us/training/modules/describe-cloud-service-types/1-introduction
- Describe IaaS (Infrastructure as a Service)
- Describe PaaS (Platform as a Service)
- Describe SaaS (Software as a Service)
- Identify appropriate use cases for each cloud service type

Describe Infrastructure as a Service (IaaS)
- IaaS is the most flexible category of cloud services
- It provides the maximum amount of control for cloud resources
- The cloud provider is responsible for maintaining the hardware, network connectivity (to the Internet) and physical security
- Customers are responsible for everything else
	- OS installation, configuration and maintenance
	- Network configuration
	- Database and storage configuration
	- and so on
- Essentially renting the hardware in a cloud datacentre, but what you do with that hardware is up to the customer
- Shared Responsibility Model
	- IaaS places the largest share of responsibility with the customer
	- The cloud provider is responsible for maintaining the physical infrastructure and its access to the Internet
	- Installation, configuration, patching and updates, security are handled by the customer
	- List of Customer Responsibilities:
		- Information and data
		- Devices (Mobile and PCs)
		- Accounts and Identities
		- Identity and Directory Infrastructure
		- Applications
		- Network Controls
		- Operating Systems
- Scenarios
	- Lift-and-shift migration
		- Setting up cloud resources similar to your own on-prem datacentre
		- Then simply moving the things running on-prem to running on the IaaS infrastructure
	- Testing and Development
		- You can start up or shut down the different environments rapidly with an IaaS structure, while maintaining complete control

Describe Platform as a Service (PaaS)
- Middle ground between renting space in a datacentre (IaaS) and paying for a complete and deployed solution (SaaS)
- The cloud provider maintains the physical infrastructure, physical security, and connection to the Internet
- They also maintain the OSes, middleware, deployment tools, and business intelligence services to make up a cloud solution
- In a PaaS scenario, you don't have to worry about the licensing or patching for OSes and databases
- PaaS is well suited to provide a complete development environment without the headache of maintaining all the development infrastructure
- Shared Responsibility Model
	- PaaS splits the responsibility between the customer and the cloud provider
		- Identity and Directory Infrastructure
		- Applications
		- Network Controls
- Scenarios
	- Development Framework
		- PaaS provides a framework that developers can build upon to develop or customise cloud-based applications
		- Similar to the way one would create an Excel macro, PaaS lets developers create applications using built-in software components
		- Cloud features such as scalability, high-availability, and multi-tenant capability are included, reducing the amount of coding that developers must do
	- Analytics or Business Intelligence
		- Tools provided as a service with PaaS allows organisations to analyse and mine their data, finding insights and patterns and predicting outcomes to improve forecasting, product design decisions, investment returns, and other business decisions

Define Software as a Service
- The most complete cloud service from a product perspective
- With SaaS you're essentially renting or using a fully developed application
- Email, financial software, messaging applications, and connectivity software are all common examples of a SaaS implementation
- While SaaS model may be the least flexible, it's also the easiest to get up and running - requiring the least amount of technical knowledge or expertise to fully employ. 
- Shared Responsibility Model
	- SaaS puts the most responsibility on the cloud provider
	- Identity and Directory Infrastructure (shared)
- Scenarios
	- Email and messaging
	- Business productivity applications
	- Finance and expense tracking
