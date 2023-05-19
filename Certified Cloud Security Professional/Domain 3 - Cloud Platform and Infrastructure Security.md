![Domain 3](images/domain3.png)

## 3.1 Comprehend cloud infrastructure and platform components

Control Frameworks
* Used to meet sec and privacy reqs as part of a governance program
* [ISO/IEC 27014:2020](https://www.iso.org/standard/74046.html)
    * Information security, cybersecurity and privacy protection — Governance of information security
    * provides guidance on concepts, objectives and processes for the governance of information security, by which organizations can evaluate, direct, monitor and communicate the information security-related processes within the organization.
* [ISO/IEC 38501:2015](https://www.iso.org/standard/45263.html)
    * provides guidance on how to implement arrangements for effective governance of IT within an organization.
* Enterprise Security Controls
    * Intended Effects Categories
        * Deterrent Controls
            * Intended to prevent an intruder from trying to access a secure area
            * Warning sign of consequences
    * Preventive Controls
        * Intended to block an intruder from accessing a secure area
        * Biometric reader at a door entry
    * Detective Controls
        * Intended to alert security personal to a potential or actual security violation
        * Security camera monitored by software or a guard
    * Mechanism of Action
        * Technical Controls
            * Use tech to deter, prevent, or detect security violations
            * Alarm system
        * Administrative Controls
            * Business processes to enhance physical security
            * Policies, standards, processes, procedures, guidelines by corp admins (executive / mid-level mgmt)
    * Compensating controls
        * Fill in known gaps in security
        * Satisfy the req for a sec measure that is too difficult to implement at the time
    * Corrective Controls
        * designed to react to the detection of incidents to reduce or eliminate
    * Recovery Controls
        * restor after an incident occurs
* ![Controls](images/controls.png)



Physical Environment
* components are physically located with the CSP but some are accessible via the network
* CSP takes on customer datacenter facilities, infra management responsibilities
* See Share Responsibility Model In [Domain 1](Domain%201%20-%20Cloud%20Concepts%2C%20Architecture%20and%20Design.md)
* Considerations
    * CSPs utilize common controls to address risks
    * physical security, standard measures such as locks, security peronnel, lights, fences, visiot check-in procedures
    * logical access controls identity and access management (IAM), single sign-on (SSO) provider, multifactor auth (MFA) and logging
    * Controls for data confidentiality and integrity like any cloud customer but with much broader controls
    * Example:
        * _Ensuring that communication lines are not physically compromised by locating telecommunications equipement inside a controlled area of the CSPs building or campus_


Network and Communications
* IaaS 
    * Customer is responsible for configuring the VMs, VPC, and guest os security as if the systems were on-prem
    * csp is responsbile for physical host, phsyical storage, and phsyical network
* PaaS
    * csp is responsible for the physical components, the internal network, and the tools provided
    * cheaper for customer, but less control
* SaaS
    * customer remains responsible for configuring access to the cloud service for their users, as well as shared resp for data
    * CSP owns physical infra, as well as network and comms

Compute
* infra components that deliver compute resources, such as VMs, disk, processor, memory and network resources
* Reservation
    * a min resource that is guarranteed to the customer
* Limits
    * max utilizatioin of compute resource by a customer (e.g. VM)
    * limits are allowed to change dynamically based on current conditions and consumption
* Shares
    * a weighting given to a particulare VM used to calculate percentage-based access to pooled resources when there is contention
    * in cases of shortage, host scoring determines who gets capacity
        * ex: Spot instances
* Responsibilities
    * CSP remains responsible for maintenance and security of the physical components
    * customer is responsible largley for their data and users

Virtualization
* security of the hypervisor is always the responsibility of the CSP
* virtual network and vm may be either csp or customer depending on the service model
* Associated Risks
    * flawed hypervisor can facilitate inter-vm attacks
    * network traffic between vms is not necessarily visible
    * resource availablity for vms can be impacted
    * vms and their disk images are simply files, can be portable and moveable
* Sec recommendations for the hypervisor (CSP resp)
    * install all updates to the hypervisor as they are released by the vendor
    * restrict admin access to the management interfaces of the hypervisor
    * capabilities to monitor the security of activity occuring between guests os
* Sec recommendations for the guest os (CPS may provide tools, but resp is on customer)
    * install all updates to the guest os promptly
    * backup the virtual drives used by the guest os on a regular basis
* Network Security
    * hypervisor security includes:
        * preventing physical access to the servers
        * limiting both local and remote access 
    * virtual network between the hypervisor and the vm is also a potential attack surface
        * responsibility is shared between csp and customer
        * components include:
            * virtual network, virtual switches, virtual firewalls, virtual ip address, etc
* Focused Attacks
    * VM Escape
        * attacker gains access to a vm, then either attacks the host machine that holds all the vms, the hypervisor, or any of the other vms
        * malicious user breaks the isolation between vms running on a hypervisor by gaining access outside their vm
        * Ensure patches on hypervisors and VMs are alway up to date
        * Ensure guest privileges are low, server-level redundancy and HIPS/HIDS protection

Storage
* CSP responsibilities
    * physical protection of data centers and the storage infrastructure the contain
    * security patches and maintenance of underlying data storage technologies and other data services they provide
* Customer responsibilities
    * properly configuring and using the storage tools
    * logical security and privacy of data they store in the CSP's environment
* Compensating Controls for lack of physical control of the storage medium (customer) includes:
    * only storing data in an encrypted format
    * retaining control of the keys needed to decrypt the data

Management Plane
* What is the management plane?
    * provides the tools (web interface/APIs) necessary to configure, monitor, and control your cloud environment 
    * provides virtual management options equivalent to the physical administration options a legacy data center would provide
        * e.g. powering VMs on/off, provisioning vm resources, migrating a vm
    * interaction is done through the CSP's cloud portal, CLI (bash, powershell), client SDKs, or via REST API
    * Seperate from and works with the **control plane** and the **data plane**
* Control Plane
    * is what you are calling when you create top-level cloud resources with ARM & Bicep (Azure), CloudFormation(AWS) or Terraform (IaC)
* Data Plane
    * performs operations on resources created through the control plane
* Management Plane Security
    * Key Interfaces
        * Cloud Portal
            * web interface of the CSP provider
            * i.e. Azure Portal, AWS Management Console, GCP Console
        * Scheduling
            * the ability to stop/start a resource at a scheduled time
            * i.e. Instance Scheduler or Lambda (AWS), Azure Automation or Function
        * Orchestration
            * automation processes to manage resources, services, and workloads, and IaC deployments
            * i.e. CLoudFormation, Azure DevOps, Cloud Build, Cloud Deployment Manager
        * Maintenance
            * update, upgrade, security pataching, etc
    * Security Controls
        * Using multi-factor auth, RBAC, and role management

## 3.2 Design a secure data center

Logical design (e.g., tenant partitioning, access control)
* Concept
    * abstraction
    * legacy co-location (CoLo) scenerio, customers were seperated at the server rack or cage-level
    * logical data center design in the cloud, customers utilize software and services provided by the CSP
    * logical design of the cloud infra should:
        * create **tenant partitioning** or isolation
        * limit and secure **remote access**
        * monitor the cloud infra
        * allow for the patching and updating of systems
* Tenant Partitioning
    * logical isolation in CSP multitenancy makes cloud computing more affordable but creates some security and privacy concerns
    * if isolation between tenants is breached, customer data is at risk
    * Multitenancy is a concept developed decades ago:
        * business centers phyically housed multiple tenants
        * colocation data centers supported multiple customers
    * risk in these scenerios is largely **physical (server, rack, cage)**
    * in public cloud, tenant partitioning is largely logical
    * customers are sharing capacity across the CSP datacenter, including physical components
    * CSP and tenant share responsibility for implementing and enforcing controls that address the unique multitenant risks of the public
* Access Control
    * single point of access makes access control simplier and facilities monitoring, but any single point can become a failure point as well
    * **hybrid identity** (single login for on-prem and cloud) can simplify identity and access management (IAM)
        * federate a customer's existing IAM system with their CSP tenant
        * facilitate IAM between cloud and on-prem resources is Identity-as-a-Service (IDaaS)
        * i.e. Azure Activie Directory (used with Office 365) or Google's Cloud Identity (used with Google Workspace)
    * Local and Remote Access Controls
        * **Remote Desktop Protocol (RDP)**
            * native remote access protocol for windows operating systems
            * supports encryption (TLS) and MFA
        * **Secure Shell (SSH)**
            * native remote access protocl for Linux OS, and common for remote management of network devices
            * supports encryption (TLS) and MFA
        * **Secure Terminal/Console-Based Access**
            * system for secure local access
            * a KVM (keyboard view mouse) system with access controls
        * **Jumpboxes**
            * a bastion host at the boundary of lower and higher security zones
            * CSPs offer services for this: Azure Bastion, AWS Transit Gateway
        * **Virtual Clients**
            * software tools that allow remote connections to a VM for use as if it is your local machine
            * e.g Virtual Desktop Infrastructure (VDI) for contractors

Physical design (e.g., location, buy or build)
* Build 
    * Requires significant investment to build a robust DC
    * offers the most control over DC design
    * Requires knowledge and skill to match quality of BUY option
* Buy
    * Generally, lower cost of entry (especially in shared scenerio)
    * Less flexibility in service design (limited to what provider offers)
    * Shared datacenters come with additional security challenges
    * Leasing space is another Buy option but limited to Rack/Cage level
* Physical Design Considerations
    * Availablility of affordable, stable, resilient electricity
    * Natural disaster exposure (flood, hurricane, tornado, etc)
    * Availability of high-speed redundant internet connectivity
    * Availability of other utilities
    * Physical site security (vehicular approaches, visibility)
    * Location relative to existing customer datacenters (BCDR)
    * Geographic location relative to customers
* Physical Security Challenges
    * strong fence line of sufficient height and construction
    * lighting of facility perimeter and entrances
    * video monitoring and alerting
    * electronic monitoring for tampering
    * visitor access procedures with controlled entry points
    * interior access controls (badges, key codes, secured doors)
    * fire detection and prevent systems
    * protection of sensitive assests, systems, wiring closets, etc.

Datacenter Tier Standard (Classification)
* List created by the [Uptime Institute](https://uptimeinstitute.com/tiers)
* Describes the level of resiliency in a facility
* Tiers
    * Tier 1
        * Basic Site Infrastructure
        * no redundancy
        * Must have:
            * Uninterruptible Power Supply (UPS)
            * 24x7 Dedicated cooling equipment 
            * Generator for extended outages
        * Expected 99.671% uptime
    * Tier 2 
        * Redundant Site Infrastructure
        * Provides partial redundancy
        * Must Have:
            * Redundant cooling components
            * Redundant power components
            * Fuel Storage
        * Expected 99.741% uptime
    * Tier 3
        * Concurrently Maintainable Site Infrastructure
        * more redundancy
        * Must Have:
            * Never require maintenance shutdowns → enough redundant components
        * Expected 99.982% uptime
    * Tier 4
        * Fault-Tolerant Site Infrastructure
        * can withstand either planned or unplanned activity without affecting availability
        * eliminates all single point of failure
        * Must Have:
            * Protected against unplanned events
            * fully redundant infrastructure including dual commercial power feeds, dual back generators
        * Expected 99.995% uptime

Environmental design (e.g., Heating, Ventilation, and Air Conditioning (HVAC),
multi-vendor pathway connectivity)
* Heating, Ventilation, and Air Condition (HVAC)
    * DC’s used to be very cold
    * Environmental threats are major risks to equipment
    * High humidity → leads to condensation that may damage electronic equipment
    * Low Humidity → leads to static electricity that may damage electronic equipment
    * Current standards for data center cooling come from the American Society of Heating, Refrigeration and Air Conditioning Engineers.  
        * The standard is called the “expanded environment envelope”
        * Maintaining proper HVAC and humidity
            * 64.4 F - 80.6F → HVAC (Expanded Envelope)
            * 41.9 F - 50 F → Humidity (Dew point Range) → Sweet Spot
    * Servers draw cool air in the front and expel hot air out back
    * ![Server hot/cold](../Certified%20In%20Cybersecurity%20(CC)/images/server.png)

    Hot/Cold aisle approach makes cooling data centers more efficient
    ![hot/cold](../Certified%20In%20Cybersecurity%20(CC)/images/hot-cold-server-aisle.png)
    * HVAC failure can reduce availability of computing resources (just like power)
    * SOC-2 Type II report can help assess HVAC concerns
        * requires NDA prior to sharing due to confidential information
* Multivendor Pathway Connectivity
    * using more than one Internet Service Provider (ISP)
    * proactive way for CSPs to mitigate risk of losing network connectivity
    * best is dual-entry, dual-provider for HA

Statements on Standards For Attestation Engagments (SSAE)
* SSAE 18 is an audit standard to enhance the quality and usefulness of System and Organization Control (SOC) reports
* designed for larger organizations, such as CSP, as the cost of a type 2 report can run $30,000 or more
* [SOC Reports Details](https://sprinto.com/blog/soc-1-soc-2-soc-3/#:~:text=SOC%201%20is%20a%20financial,presented%20to%20a%20general%20audience)
* SOC Reports
    * SOC 1 - internal controls over financial reporting
        * Type 1 - financial audits at a point in time
        * Type 2 - financial audits over a period of time
    * SOC 2 - Security, processing, integrity, availability, privacy controls (requires NDA) 
        Type 1
        * report that assesses the design of security processes at a specific point in time
        * Type 2
            * ofter seen as Type II
            * assesses how effective those controls are over time by observing operations for six months
    * SOC 3 - same as soc 2 but watered down and is publicly available

Design Resilient
* resislent designs are engineered to respond positively to changes or disturbances, such as natural disasters or man-mad disturbances
* Examples:
    * HA firewalls, active-passive or active-active
    * Mutli-vendor pathway connectivity
    * Web Server Farm (behind redundant Load Balancers)
    * Database Cluster (windows/linux cluster feature)


## 3.3 Analyze risk associated with cloud infrastructure and platforms

Risk assessment (e.g., identification, analysis)
* **Risk Management Process** is fundamental to information security since the entire practice involves **mitigating and managing risk** to data and info systmes
* Risk Frameworks
    * [ISO/IEC 31000:2018](https://www.iso.org/standard/65694.html) - Risk Management Guidelines
    * [NIST SP 800-37](https://csrc.nist.gov/publications/detail/sp/800-37/rev-2/final) - Guide for Applying the Risk Management Framework to Federal Information Systems
* Identification
    * First step in the process
    * Once assets are identified then sec practitioners and risk managers can then begin to identify potential causes of disruption to the assets
* Analysis
    * Analyzing identified risks continues the conversation start by "What could go wrong?"
    * Assessment Types
        * Quantitative
            * Assigns a dollar value to evaluate effectiveness of countermeasures
            * Uses objective numberical ratios to evaluate risk likelihood and impact
    * Analysis seeks to answer two questions:
        * "What will the impact be if that goes wrong?":
            * Single Loss Exectancy (SLE) - $
        * "How significant will the loss be?":
            * Exposure Factor (EF) - %
        * "How likely is it to happen?":
            * Annualized Rate of Occurrence (ARO) - decimal (%)
            * Ex:
                * An impact that happens _twice a year_ has an ARO of **2.0**
                * An impact that happens _once every two years_ has an ARO of **0.5**
                * An impact that happens _once every five years_ has an ARO of **0.2**
        * With the SLE and the ARO you can determine the Annualized Loss Expectancy (ALE)
            * Formula ALE = SLE x ARO
        * Scenerio 1:
            * Issue: It is estimated a tornado may strike a branch office once every 5 years, causing 30% loss to a $1,000,000 building
            * Calculate the cost of Single Occurence (SLE)
                SLE = Assess Value (AV) x EF
                Ex: $1,000,000 (AV) x 0.30 (EF) = $300,000 (SLE)
            * Calculate the annualized lost cost (ALE)
                * SLE = $300,000
                * ARO = 0.2 (once every five years)
                * Ex: $300,000 x 0.2 = $60,000 (ALE)
    * Analysis of CSP Risks
        * CSP Focus Areas
            * Business Units
            * Vendor Management
            * Privacy
            * Information Security
        * Standards for CSP Guidance
            * [ISO/IEC 27001](https://www.iso.org/standard/27001)
                * framework for policies and procedures that include legal, physical, and technical controls involved in an organization's information risk management processes
            * [ISO/IEC 27017](https://www.iso.org/standard/43757.html)
                * security standard developed for CSPs and users to make a safer cloud-based environment and reduce the risk of security problems
            * [ISO/IEC 27018](https://www.iso.org/standard/76559.html)
                * first international standard about the privacy in cloud computing services
                * code of practice for protection of PII in public clouds acting as PII processors
    * Data Privacy and Infor Sec Risks:
        * Authentication Risk
        * Data Security
        * Supply Chain Risk Management (SCRM)
* losing ownership and full control over system hardware assets
* SLAs are critical to limit risk
* Common Cloud Risks
    * Geographic dispersion of the CSPs data centers
        * if properly architect a disruption at one DC should not affect or cause a complete outage
    * Downtime 
        * resiliency in network connectivity, zonal and regional
    * Compliance
        * jurisdictions may demand that data may not be dispered
        * dictate data privacy (GDPR)
    * General technology risk
        * cloud systems are not immume to standard security issues like cyberattacks
        * CSPs defenses should be documented and tested and customers aware of their configuration responsibilities
* Risk Types
    * External
        * different threat actors, ranging from competitors and script kiddies to crime syndicates and state actors
        * capabilities depend on tools, experience, and funding
        * environmental threats (fires, floods)
        * man-made threats (accidental deletion of user data)
    * Internal
        * malicious insider (dissatisfied employee)
        * human error

Cloud Vulnerabilities, Threats and Attacks
* [The CSA Egregious 11](https://cloudsecurityalliance.org/artifacts/top-threats-to-cloud-computing-egregious-eleven/)
    * detailed list of top cloud-specific threats
    1. Data Breaches
        * unintentional loss/oversharing is a "data leak"
        * loss of sensitive data 
    2. Misconfiguration and inadequate change control
        * remediate through change and config management
    3. Lack of cloud security architecture and strategy
    4. Insufficient identity, credential access and key management
    5. Account hijacking
        * credential theft, abuse, and/or elevation to carry out an attack
        * likely phishing
    6. Insider threat
        * job rotation, privelege access management, audit, and security training
    7. Insecure interfaces and APIs
        * mfa, rbac, api management plaftorms, key-base API access
    8. Weak control plane
    9. "Metastructure" and "applistructure" failures
        * vulnerabilities in the operational capabilities that the CSPs make available, like APIs for accessing various cloud services
        * if CSP has inadequately secures these interfaces any resulting solutions built on top of those services will inherit these weaknesses
        * **Metastructure**
            * protocols and mechanisms that provide the interface between the cloud layers, enabling management and configuration
        * **Applistructure**
            * applications deployed in the cloud and underlying application services used to build them
            * ie. Message QUeus, functions, message services
    10. Limited cloud usage visibility
        * referes to when organizations experience a significant reduction in visibility over their info tech stack
            * IaaS vs PaaS vs SaaS
    11. Abuse and nefarious use of cloud services
        * low cost and high scale of compute in the cloud is advantage to enterprises, its an opportunity for attackers to execute disruptive attacks at scale
        * DDoS, phishing

Risk Mitigation Strategies
* select qualified CSP
* design and architecting with security in mind
* use of encryption to secure data at rest and in transit (TLS)
* ongoing monitoring and management to maintain posture
* Defense in depth

## 3.4 Plan and implementation of security controls

Physical and Environmental protection (e.g.,
on-premises)
* The North American Electric Reliability Corporation Critical Infrastructure Protection (NERC CIP) plan is a set of standards aimed at regulating, enforcing, monitoring and managing the security of the Bulk Electric System (BES) in North America
* Considerations
    * site location is primary
    * requirements
        * ability to restrict physical access at multiple points
        * ensuring a clean and stable power supply
        * adequate utilities like water and sewer
        * the availability of an adequate workforce
    * CSP responsibilties in the cloud , customer responsible for on-prem (private)
* Site Selection & Facility Design
    * visibility, composition of the surrounding area, area accessibility, and teh effects of natural disasters
    * customers should focus on selecting CSP datacenter locations to meet DR and data residency
    * CSPs auto-select region pairs for redundancy

Fire Suppression (Extinguisher)
* Class A
    * fires known as common combustible fires and include burning of wood, paper, cloth, or plastic
    * use water or soda acid to suppress
* Class B
    * considered liquid fires and include buring of gas, oils, tars, solvents, and alcohol
    * cannot use water, instead take the oxygen away by using CO<sub>2</sub> or FM-200 extinguisher
* Class C
    * fires include burning of elctrical components and equipement
    * previously these could be extinguished with Halon gas, CO<sub>2</sub>, or nonconductive agent such as FM-200.
    * Halon is no longer recommended becuase of the ozone depletion
    * CO<sub>2</sub> and FM-200 can still be used
* Class D
    * fires include burning of combustible metals such as magnesium and sodium and requires the use of dry chemcials to suppress
* Class K
    * Kitchen fires (fats / oils)
    * Use same as class b extinguisher
    * Class F in Europe and Australia

![Fire Extinguishers](../Certified%20In%20Cybersecurity%20(CC)/images/fire-extinguisher-types.webp)


Other Suppression
* Wet Pipe
    * water is in the pipe at all the time and ready to be released
    * drawback is pipe could break and release the water and DC could be flooded
* Dry Pipe
    * water sitting in a reservoire and not in the pipe
    * after a short delay the water is released when a value is turned (maunally or auto)
* Pre-action system
    * head link on the sprinkler has to be melted in order for the water to be released

Other environmental issues to protect against
* Protect against flooding → choose a location that flooding rarely occurs or not at all
* Use moisture sensors to prevent water infiltration
* Electromagnetic Interference
    * Generated by all electronic equipment
    * Interferes with normal operation of other equipment
    * Enables eavesdropping attacks → attackers can reconstruct keystrokes (side channel attack)
    * Use faraday cages to control EMI → rarely used outside of government builds

System, Storage and Communication Protection
* [NIST SP 800-53](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final)
    * Security and Privacy Controls for Information Systems and Organizations
    * Contains a family of security, privacy, and protection controls specific to systems and communications
* Protection (Technology)
    * Encrypt and protect data (at rest, in transit, in use)
    * Protect systems and services (DoS/DDoS, Boundary (ingress/egress), Key Management)
* Security Practices (People/Processes)
    * Automation configuration
    * Responsibilities for protecting cloud systems and services
    * Monitoring and maintenance
* Concepts
    * Policy and Procedures
        * Establish requirements for system protection, and define the purpose, scope, roles, and responsibilities needed to achieve it
    * Separation of System and User Functionality
        * basic security principle that ensures that no single person can control all the elements of a critical function or system
        * seperating user and admin functions can also prevent users from altering processees or misconfiguring systems
    * Security Function Isolation
        * Example of Separation of duties
    * Denial-of-Service Protection
        * AWS Shield, Azure DDoS, Google Cloud Armor
    * Boundary Protection
        * deals with both ingress and egress protections, including:
            * Preventing malicious traffic from entering the network
            * Preventing malicious traffic from leaving your network
            * Protecting against data loss (exfiltration)
            * Configuring rules/policies in routers, gateways, or firewalls
    * Cryptographic Key Establishment and Management
        * Use TLS / VPN
        * Hashing / digital signatures
        * HMAC -- simultaneously verifiy both data integrity and message authenticity
            * sometimes expanded as either keyed-hash message authentication code or hash-based message authentication code 
            * a specific type of message authentication code (MAC) involving a cryptographic hash function and a secret cryptographic key.
            * ![HMAC](images/HMACDiagram.webp)

Identification, Authentication and Authorization
* Authentication (AuthN)
    * proces of providing that you are who you say you are
    * proof of identity
    * Permissions, rights, and privileges are granted to users based on their proven identity
* Authorization (AuthZ)
    * is the act of granting an authenticated party persmission to do something
    * granting access
    * access decisions are made using Policy Enforcement Point (PEPs)
    * individual policies are controlled at Policy Decision Point (PDP)
    * if user has assigned rights to a resource, they are granted authorization
    * principle of least privelege
* Accountability
    * users who perform activities on a system are held accountable, typically enforece with adequate logging and monitoring of system activity
    * challenges in enforcing accountability in the cloud
        * SaaS apps used as users travel make identifying anomalous / malicious behavior more difficul
        * Bad Password practices (reuse across services)
        * Use of personal devices in BYOD scenerios
    * Modern IDaaS tools provide solutions for the above challenges
* Multifcator Authentication (MFA)
    * works by requiring two or more of the following authentication methods:
        * Somethiing you **know** (pin or password)
        * Something you **have** (trusted device, soft/hard token)
        * Something you **are** (biometric)
    * Factors and Attributes
        * passwords are the weakest form of authentication
        * password policies help increase their security by enforcing complexity and history requirements
        * Smartcards include microprocessors and cryptographic certificates
        * Oath tokens create one-time passwords (OTP)
        * Biometric methods identify users based on individual characteristics such as fingerprints and facial recognition
    * Conditional Authentication Policies
        * ![Conditional Auth](images/conditional-auth-policies.png)
        * Benefit
            * allows Administrator the ability to build conditions that manage security controls that can block access, require multifactor authentication, or restrict the user's session when needed and stay out of the user's way when not
    * Authentication Methods
        * Authentication Applications 
            * Authenticator Apps
            * software-based authenticator that implements two-step verification services using the Time-based One-Time Password Algorithm and HMAC-based One-Time Password algorithm, for authenticating users of software applications
            * Examples include Microsoft Authenticator and Google Authenticator
            * using opend standards developed by the [Initiative for Open Authentication (OATH)](https://en.wikipedia.org/wiki/Initiative_for_Open_Authentication)
        * Push Notifications
            * server is pushing down the authentication information to a mobile device
            * uses the mobile device app to be able to recieve the pushed message and display the authentication information
* Concepts of Federated Services
    * Federation
        * collection of domains that have **established trust**
        * level of trust may very, but typically includes authentication and almost always includes authorization
        * Oftern includes a number of organizations that have established trust for shared access to a set of resoruces
        * Example:
            * you can federate you on-premises environment with Azure AD and use this federation for authentication and authorization
            * This sign-in method ensures that all users authencation occurs on-premises
        * Allows administrators to implment more rigorous levels of access control
        * Certificate Authentication, key fob, card token
        * ![Federation](images/federation.png)
    

Audit mechanisms (e.g., log collection,
correlation, packet capture)
* Log Collection
    * cloud services will offer different controls over what information is logged
    * min level of security-related events such as use of or changes to privilege accounts
    * log aggregator can ingest logs from all on-premises and cloud resources for review
    * NIST SP 800-53 and OWASP logging cheet seet offer guidance on specific information to capture in audit reocrds
* Correlation
    * ability to discover relationships between two or more events across logs
    * commonly associated with a SIEM
* Packet Capture and Replay 
    * tools are called **protecol analyzers**
    * cloud environment may not provide any facility for capturing packets, particularly in SaaS scenerios
    * Allow deep inspection of traffic
    * Troubleshoot network issues
    * Investigate security incidents
    * Eavesdrop on confidential communications
    * In the cloud
        * CSP must partition network traffic to prevent users from eavesdropping on each other
        * CSP must retain the capability to observe all traffic themselves
        * Customers must understand the limitations of their own packet captures
    * Example tools
        * NetFlow 
            * a network protocol developed for Cisco routers by Cisco Systems, is widely used to collect metadata about the IP traffic flowing across network devices such as routers, switches and hosts. The traffic flow data informs a company’s IT professionals as to how much traffic there is, where it’s coming from and going to, and the paths being used.
        * Wireshark
            * a free, open-source protocol analyzer, with CLI and GUI verisons, available for Windows and Linux (including macOS)
            * some CSPs support Wireshark, others have specificalized services to perform packet capture on virtual networks
                * e.g Network Watcher (Azure), AWS supports Wireshark
            * Some CSP protocol analyzers can save the data that they collect to a Wireshark-compatible packet capture file (PCAP)
        * Tcpdump
            * Command line open source protocol analyser
                * `$ tcpdump -n -i eth0 ‘tcp port 22’`
            * Tcpdump → https://www.tcpdump.org/
            * Wireshark and tcpdump are built using libpcap library → https://github.com/the-tcpdump-group/libpcap
        * Tcpreplay → allows editing and replaying traffic


## 3.5 Plan business continuity (BC) and disaster recovery (DR)

Business Continuity Plan (BCP)
* Business-focused
* org plan for "how-to" continue business after an event has occurred
* proactive risk mitigtion strategy that contains likely scenerios that could affect the organization and guidance on how the organization should respond
* sometimes referred to as _Continuity of Operations Plan (COOP)_
* focuses on the whole business
* cover communications and process more broadly
* Definitions
    * Business Resumption Plan (BRP)
        * plan to move from disaster recover site back to normal operating business environment
    * Mean Time Between Failures (MTBF)
        * a time determination for how long a piece of IT infrastructure will continue to work before it fails
    * Mean Time To Repair (MTTR)
        * a time determination for how long it will take to get a piece of hardware/software repaired and back on-line
    * Max Tolerable Downtime (MTD)
        * amount of time we can be without the asset that is unavailable **BEFORE** we must declare a disaster and initiate the DR plan

Disaster Recovery Plan (DRP)
* focuses more on the technical aspects of recovery
* plan for recovering from an IT disaster and having the IT infrastructure back in operation

BCP/DRP From a CSP Perspective
* cloud data center that is affected by a natural disaster will likely activate multiple BCPs and DRPs
* CSP will activate both plans to deal with the interruption to their service
* one key element of the BCP is communication incident status to relevant parties

BCP/DRP From a Customer Perspective
* customer responsibility for determinig how to recover in the case of a disaster in the cloud
* customer may choose to implement backups, or utilize multiple availability zones, load balancers, or other techniques
* CSPs can further protect customers by not allowing two availability zones within a single phyiscal datacenter within a cloud region
    * Availability Zones
        * unique physical locations within a region with independent power, network, and cooling
        * comprised of one or more datacenters
        * tolerant to datacenter failures via redundancy and isolation

Communication Plan
* plan details how relevant stakeholders will be informated in event of an incident (i.e. security breach)
* inlcude maintaining confidentiality such as encryption to ensure that the event does not become public knowledge
* contact list should be maintained that includes stakeholders 
from the government, police, customers, suppliers and internal staff
* compliance regulations, like GDPR, include notification requirements, relevant parties and timelines
* Stakeholders
    * **stakeholder** is a party with an interest in an enterprise; corporate stakeholders include investors, employees, customers, and suppliers
    * Communication Plan should contain the relevent groups
        * Internal stakeholders
        * Cyber Insurance Provider
        * Business Partners
        * Customers
        * Law enforcement (not mandatory unless a criminal law is broken)

Business requirements (e.g., Recovery Time Objective (RTO), Recovery Point Objective (RPO),
recovery service level)
* Recovery Point Objective (RPO)
    * age of data that be recovered from a backup storage for normal operations to resume if a system or network goes down
* Recovery Time Objective (RTO)
    * duration of time and a service level within which a business process must be restored after a disaster in order to avoid unacceptable consequences associated with a break in continuity
* Recovery Service Level (RSL)
    * measures that compute resources needed to keep production environments running during a disaster
    * percentage measure (0-100%) of how much computing power that will be needed during a disaster
    * based upon a percentage of computing used by producution environment versus others, such as dev, test, and QA
    * Example: a 10-web server environment that uses 8 for dev, test, and QA, only 2 would need to be migrated for production

BCDR Planning Factors
* Important Assets: Data and Processing
* Current location of the assets
* The network between the assets and the sides of their processing
* Actual and potential location of the workforce and business partners concercing disaster event

BCDR Types
* On-Prem, Cloud as BCDR
    * CSP serves as endpoint for failover services
* Cloud Consumer, Primary Cloud Service Provider BCDR
    * One CSP region fails, service is restored in another zone of the CSP's cloud environment (region pairs)
* Cloud Consumer, Alternative Provider BCDR
    * Failure happends, restoration is done in another CSP
    * Azure is primary, DR is in Aws or GCP

BCDR Plan Creation, Implementation and Testing
* Creation of the Plan
    * Business Impact Analysis (BIA) provides input into the plan
    * Steps
        * Scope of the BCDR Plan
        * Gathering Requirements and Context
            * BIA, RPO, RTO
        * Analysis of the Plan
            * translate BCDR requirements into input to be used in the design phase
        * Risk Assesment
            * assessed for residual risk
        * Plan Design
            * objective into establishing and evaluate candidate architecture solution
* Implementation of the Plan
    * identify key personnnel is a crucial implementation steps
    * use the design in the plan to implement protections to critical business functions
    * customers can take advantage of the cloud's high availability features like:
        * mulitple az's
        * automatic failover to backup region(s)
        * direct connection to a csp
* Testing the Plan
    * ensures both the BCP/DRP function as expected and that people know their roles and responsibilities
    * testing both BCP and DRP is essential
* Report and Revise
    * BCR/DRP should be revised as necessary based on test results and business changes

BCP/DRP Test Scenarios
* BCDP and DRP should be tested **at least annually**
* Common disaster scenarios include the follwoing:
    * Data breach
    * Data loss
    * Power outage or loss of other utilities
    * Network failure
    * Naturual disasters (e.g., fire, flooding, tornado, hurricane, or earthquake)
    * Civil unrest or terrorism
    * Pandemics
* Testing Types
    * Checklist Review
        * distribute copies to BCP/DRP to managers of each critical business unit asking them to review
    * Tabletop testing / Walk Through Test
        * primary objective is to ensure that critical personnel are aware of BCP and plan accurately reflects the organization's ability to recover from disaster
        * role play a disaster scenerio
        * scenerion is  only known to the test moderator
        * team members refere to the document and discuss the appropriate response to that particular type of disaster
        * minimal import on productivity
    * Dry Run / Walk Through Drill / Simulation Test
        * some of the responses measures are tested (on-non critical functions)
        * More involved than tabletop.
        * Participants choose a scenario and apply BCP to it
    * Functional Drill / Parralel Test
        * People move to an offiste locatoin to see if BCP is properly invoked
        * operations are NOT switched
    * Full Test
        * involves actually shutting down operations at the primary site and shifting them to the recovery site
        * when the entire organization takes part in an unscheduled, unannounced practice scenario, of full BC/DR activities

