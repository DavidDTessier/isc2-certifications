# Domain 7 - Security Operations

## 7.1 - Understand and comply with investigations

* Evidence collection and handling
* Reporting and documentation
* Investigative techniques
* Digital forensics tools, tactics, and procedures
* Artifacts (e.g., data, computer, network, mobile device)

## 7.2 - Conduct logging and monitoring activities

* Intrusion detection and prevention (IDPS)
* Security Information and Event Management (SIEM)
* Continuous monitoring and tuning
* Egress monitoring
* Log management
* Threat intelligence (e.g., threat feeds, threat hunting)
    ** * occurs when threats cant be predicted due to unforeseen issues
        * also known as _threat hunting_ 
        * activity of looking for existing evident of a compromise once symptoms or indicators of compromise (IOCs) of an exploit become known.
        * uses IoC information to find harm that has already occurred
* User and Entity Behavior Analytics (UEBA)

## 7.3 - Perform Configuration Management (CM) (e.g., provisioning, baselining, automation)

* _**Configuration Management (CM)**_
  * ensures that systems are deployed in a secure, consistent state and they remain in a secure and consistent state throughout their lifetime
  * Baselines and images are commonly used to deploy systems
* **Provisioning**
  * refers to installing and configuring the OS and needed applications
  * deploying the OS and applications using a secure configuration will help reduce any vulnerabilities
  * Common Hardening includes
    * Disable all unused services
      * ie. FTP is rarely used and should be disabled
    * Close all unused logical ports
      * often closed by disabling unused services
    * Remove all unused applications
      * some are added automatically and should be removed if unneeded
    * Change default passwords
* **Baselining**
  * starting point for a system
  * admins can and should modifying settings to meet org requirements
  * improves overall security ensuring that desired security settings are always configured correctly
  * reduce deployment time and maintenance
  * baseline images should be secure stored to avoid tampering (injection of malware of vulnerabilities)
  * **_Images as Baselines_**
    * images are typically used to deploy baselines
    * typical three-step process
      * (1) Admin installs the OS and desired applications on a computer (or vm) as the baselining system. Configures relevant security settings to meet the org's needs. Extensive testing is done to ensure the system operates as expected
      * (2) Admin then captures an image of the system using imaging software and stores in on a server (image server) or on a external hard drive, USB drives, or DVDs
      * (3) Personnel then deploy the image to systems as needed. These systems often require additional configuration to finalize them, such as giving them unique names, overall sys config is the same
* **Automation**
  * imaging is typically combined with other automation tools
  * integrated with tools like `Ansible` and `Terraform` for automation of infra provisioning and configuration
  * Microsoft's Group Policy (GP)
    * admins can configure a GP setting one time and automatically have the setting applied to all computers in the domain
    * can we used to modify specific Windows Registry settings
    * susceptible to Powershell privilege escalation attacks

## 7.4 - Apply foundational security operations concepts

### Least privilege and Need-To-Know

* two standard principles to following in IT security
* help protect valuable assets by limiting access
* related and sometimes interchangeable but have differences
* **_Principle of Least Privilege_**
  * subjects are granted only the privilegeds necessary to perform their assigned work tasks
  * includes both permissions and rights
  * for data this means controlling the ability to read, write, create, alter, and delete
  * ensures protection of confidentiality and data integrity
  * works on the assumption of well defined job descriptions for users
  * this is typically violated when all users are added to the local Admin group or granting root access to a computer
    * problems if the use logs in to a system as root/admin and accidentally installs malware on to the system
  * also used in context of applications and services
    * service accounts should have limited scope and permissions for what they need to do
* **_Need-To-Know Principle_**
  * imposes the requirement to grant users access to only the data or assets/resources they need to perform assigned work tasks
  * primary purporse is to keep secret information secret and limit who knows the secret
  * commonly associated with security clearences, but the clearence doesnt automatically grant them access to the secret data
    * admins grant them access to only the data on a "need-to-known" basis for their job
  * primarily for military and government agencies, but can be utilized for civilian organizations
  * helps protected against unauthorized access that could result in loss of confidentiality

#### Segregation of Duties (SoD) and Responsibilities

* aka "separation of duties"
* ensures that no single person has total control over a critical function and/or system
* creates "checks-and-balances" systems where two or more users verify each other's actions and must work in together to accomplish necessary work tasks
* more difficult for engaging in malicious, fraudulent, or unauthorized activities
* may lead to the risk of collusion between two or more people to compromise the organization
  * fraud detection is increase and acts as an effective deterrent
* typically tasks are broken up to prevent fraud
  * example:
    * one person approves payment for a valid invoice, but someone makes the payment
    * dividing admin capabilities/functions among multiple trusted individuals
* **Two-Person Control**
  * aka "two-man rule"
  * requires the approval of two individuals for critical tasks
  * example:
    * two keys are required to open a safe, the keys are split between two people
  * _**Split knowledge**_
    * concept which combines both the concept of segregation of duties and two-man rule in to one
    * used in key escrow
    * infomration of privilege to perform a task is split between two or more users, ensuring no single person has sufficent privileges to compromise the security of the environment

### Job Rotation

* aka "rotation of duties"
* employees rotate through jobs or rotate job responsibilities with other employees
* necessary security control provides peer review, reduces fraud, and enables cross-training
* policy can act as both a deterrent and a detection mechanism
  * if employees know that someone else will be taking over their job responsibilities in the future, they are less likely to take part in fraudulent activities

### Mandatory Vacations

* require employees to take _mandatory vacations_ in one- or two-week increments
* provides a form of "peer review" and helps detect fraud and collusion
* policy helps ensure that another employee takes over an individual's job responsibilities for at least a week
  * if a person is involved in fraud, the other will likely detect it
* acts as both deterrent and detection mechanism (like job rotations)

### Privileged Account Management

* aka PAM
* solutions that monitors and restricts access to privileged accounts/permission or detect when accounts use any elevate privileges
* Microsoft domains include a PAM solution, base on "Just-in Time" admin principle
* users are placed in a privilege group, but members of the group don't have elevated privileges
* they request permissions to use elevate privileges when they need them
* PAM admins approve/denies this request behind the scenes and granted (if approved) in seconds by issuing a time-limited ticket
* after a time the ticket expires and the privileges are revoked

### Advanced Persistent Threat (APT)

* APT is a prolonged, sophisticated, and targeted cyberattack where a threat actor gains unauthorized access to a network and stays undetected for an extended period.
* APT's are methodical, patient, and highly focused, often carried out by well-funded, skilled adversaries, such as state-sponsored groups or large criminal organizations.
  * not a "hit-and-run" attacks
* goal of a APT is not usually immediate financial gain, but rather to steal sensitive data, conduct cyber espionage, or disrupt operations over time.
* An APT attack typically unfolds in several distinct stages:
  * **Reconnaissance**: Attackers thoroughly research their target to find vulnerabilities, map the network, and identify key personnel.
  * **Initial Compromise**: They gain an initial foothold, often through spear-phishing emails, exploiting software vulnerabilities (including zero-days), or using stolen credentials.
  * **Establishing a Foothold**: Once inside, attackers deploy custom malware or backdoors to ensure they can maintain access to the network, even if their initial entry point is discovered.
  * **Lateral Movement and Privilege Escalation**: The attackers move quietly through the network, escalating their privileges to gain access to more sensitive systems and data.
  * **Data Exfiltration or Disruption:** The final objective is achieved, whether it's stealing data, causing sabotage, or simply maintaining a long-term presence for future operations.
* The "Advanced," "Persistent," and "Threat" components of the term define the nature of the attack:
  * **Advanced**: The use of specialized, sophisticated tools and techniques designed to evade traditional security defenses.
  * **Persistent**: The attack is a continuous, sustained effort by the adversary to maintain a long-term presence within the target's network.
  * **Threat**: The attack is carried out by a skilled, well-resourced, and highly motivated adversary with a specific objective.
* **_Technical Alert -_** [_**TA17-239A**_](https://www.cisa.gov/news-events/alerts/2017/10/20/advanced-persistent-threat-activity-targeting-energy-and-other-critical-infrastructure-sectors)
  * released by the US Department of Homeland Security (DHS) and The Federal Bureau of Investigation (FBI)
  * describing the activities of an APT targeting energy, nuclear, water, aviation, some critical manufacturing sectors, and government entities
  * details how the attackers infected a single system with a malicious phishing email or by exploiting server vulnerabilities
  * once exploited, the escalated their privileges and began performing many common privileged operations, including
    * Accessing and deleting logs
    * Creating and manipulating accounts (such as adding new accounts to the admin group)
    * Controlling communication paths (opening port 3389 for RDP access, and/or disabling the host firewall)
    * Running various scripts (Powershell, bash, javascript)
    * Creating and scheduling tasks (such as one that logged their accounts out after 8 hours to mimic the behavior of a regular user)
* Monitoring privileged accounts/access can detect these early in their attack, if undetected APTs can remain embedded in the network for years

### Service-level agreements (SLA)

* SLA is an agreement between an organization and an outside entity, such as a vendor
* It stipulates performance expectations and often includes penalties if the vendor doesn't meet them
  * such as uptimes and downtimes
* Sometimes a _Memorandum of Understanding (MOU)_ is used, which documents the intention of two entities to work together toward a common goal
  * MOU is a less formal version of an SLA, doesn't include any penalties if one party doesn't meet the expectations

## 7.5 - Apply resource protection

* **Media Management**
  * refers to the steps taken to protect media and data stored on it
  * media includes tapes, optical media such as CDs/DVDs, portable USB drives, internal hard drives, solid state drives, USB flash drives
  * backups are often contained on tapes but extends to any type of hard-copy data
* **Media Protection Techniques**
  * for sensitive information, should be stored in a secure location with strict access controls (prevent unauthorized access)
    * also should have temperature and humidity controls to prevent loss due to corruptions
  * restrict access to devices from computer systems (block and record attempts at USB connectivity)
    * USBs are risks for malware installation and data theft
    * some organizations will only allow specific brands
      * [IronKey](https://en.wikipedia.org/wiki/IronKey)
        * includes
          * multiple levels of built-in protection
          * several authentication mechanisms to ensure only authorized user can access the data
          * strong encryption with built-in AES 256-bit hardware encryption
          * active antimalware
  * proper media management ensures confidentiality, integrity, and availability
  * **_Tape Media_**
    * used for storing backups
    * highly susceptible to loss due to corruption
    * keep at least two copies (one on-site for immediate usage, and another at a secure storage location off-site)
    * cleanliness of storage area will directly affect the life span and usefulness of tape media
    * should not be exposed to magnetic fields
    * useful guidelines
      * new media should be kept sealed in original packaging until its needed to protect from elements
      * take extra caution when opening a media package as to not damage the media
      * avoid exposing the media to extreme temperatures (not stored near heaters, radiators, ACs, etc)
      * do not use media if its damaged, exposed to abnormal levels of dust/dirt, and/or dropped
      * media should be transported from one site to another in a temperature-controlled vehicle
      * media should be protected from exposure to the outside elements (sunlight, moisture, heat/colde)
        * should acclimatize for 24 hours before use
      * appropriate security should be maintained over the media from the point of departure to the secured off-site (media is susceptible to theft/damage/tampering during this time)
      * appropriate security should be maintained over the media during its lifetime based on classification level of data on the media
      * consider encrypting backups to prevent unauthorized disclosure of data
  * **_Mobile Devices_**
    * includes laptops, smartphones, tablets, smartwatches
    * have internal memory/storage and/or removable memory cards
    * use security best practices, strong encryption
* Data at rest/data in transit

## 7.6 - Conduct incident management

* Detection
* Response
* Mitigation
* Reporting
* Recovery
* Remediation
* Lessons learned

## 7.7 - Operate and maintain detection and preventative measures

* Firewalls (e.g., next generation, web application, network)
* Intrusion Detection Systems (IDS) and Intrusion Prevention Systems (IPS)
* Whitelisting/blacklisting
* Third-party provided security services
* Sandboxing
* Honeypots/honeynets
* Anti-malware
* Machine learning and Artificial Intelligence (AI) based tools

## 7.8 - Implement and support patch and vulnerability management

* **Patch Management**
  * _patch_ is a blanket term for code written to fix/correct a bug or vulnerability or to improve software/system performance
    * referred to updates, quick fixes, and hot fixes
    * in security, admins are primarily concerned with security patches (which affect a system's vulnerability)
    * vendors write and provide patches, but they are only useful if they are applied
  * ensures that systems are kept up-to-date with current _patches_
  * Common Steps:
    * **Evaluate patches**
      * vendors announce and release a patch
      * admins review and evaluate them to determine if they apply to their systems
    * **Test patches**
      * whenever possible, admins test the patch in a controlled/isolated nonproduction system to determine if the patch causes any unwanted side effects
        * system no longer starts or is stuck in a reboot cycle
        * if it affects one system its manageable but rollout to an entire fleet could be catastrophic
    * **Approve the patches**
      * once tested, follows the Change Management Process for approval
    * **Deploy the patches**
      * after test/approval, admins deploy the patches
      * typically done in a rollout fashion to limit the blast radius
      * automated process
    * **Verify the patches are deployed**
      * regularly test and audit the system to ensure they remain patched
      * possibly also incorporate vulnerability assessment
  * **_Patch Tuesday and Exploit Wednesday_**
    * Microsoft, Adobe, and Oracle typically release patches on the second Tuesday of every month (commonly referred to as _patch tuesday_)
    * allows admins to plan for the release of patch to give them adequate time to test/deploy
    * some vulnerabilities are extreme and microsoft releases them "out-of-band" (earlier than Tuesday)
    * attackers know that organizations dont patch right away, some have even reverse-engineered the patches to identify the underlying vulnerability and then created methods to exploit it (usually a day after "exploit wednesday")
* **Vulnerability Management**
  * refers to the regularly identifying vulnerabilities, evaluating them, and taking steps to mitigate risks associated with them
  * works in conjunction with Patch Management
  * not possible to eliminate risks, not is it possible to eliminate all vulnerabilities
  * effective vulnerability management ensures the organization is regularly evaluating and mitigating vulnerabilities that represent the greatest risk
  * Most Common Vulnerability
    * unpatched systems
  * Common elements
    * _Routine Vulnerability Scans_
    * _Periodic Vulnerability Assessments_
  * **Vulnerability Scanners**
    * tools used to test systems and networks for known security issues
    * enumerates all the vulnerabilities in a system
    * sometimes used by attackers to detect weakness in systems/networks in order to exploit them
    * typically generates a report with details which are passed on to the teams performing patch management and managing the systems
    * Management may choose to accept the risk rather than mitigate it (residual risk) for business decisions
* **Common Vulnerability and Exposures (CVE)**
  * CVE is a dictionary that provides a standard convention used to identify and describe vulnerabilities
  * commonly used by patch management and vulnerability management tools
  * Example:
    * [`CVE-2020-0601`](https://www.cve.org/CVERecord?id=CVE-2020-0601)
      * identifies a vulnerability in the windows CryptoAPI (`Crypt32.dll`)
      * Microsoft patched this vulnerability in Jan 2020 security updated
  * [MITRE Corporation](https://www.mitre.org/) maintains the [CVE Database](https://www.cve.org)
    * MITRE founders have a history as research engineers at Massachusetts Institute of Technology (MIT) but is NOT part of MIT
    * receives funding from the US DHS, and Cybersecurity and Infrastructure Security (CISA) to maintain the CVE database

## 7.9 - Understand and participate in change management processes

* **_Change Management_**
  * ensures that changes do not cause outages (intentional and/or unintentional) and that appropriate personnel review and approve changes before implementation and ensure that personnel test and document the changes
  * prevents unauthorized changes (which directly affect availability)
  * formal process designed to ensure that changes to IT systems and services are made in a controlled and efficient manner, with minimal disruption to the business.
  * mandatory element for some _Security Assurance Requirements (SARs)_ in the [ISO Common Criteria](https://en.wikipedia.org/wiki/Common_Criteria)
  * [Information Technology Infrastructure Library (ITIL)](https://www.ibm.com/think/topics/it-infrastructure-library)
    * comprehensive framework of best practices for IT service management (ITSM).
    * ensures alignment of IT services with business needs, ultimately delivering value to an organization and its customers.
    * provides a structured approach to managing IT services throughout their entire lifecycle, from design to retirement.
    * not a rigid set of rules, but rather a flexible framework that an organization can adapt to its specific needs.
    * Change management is a core practice within the ITIL framework, particularly in the _**Service Transition stage (in ITIL v3/2011)**_ and the broader Service _**Value System (in ITIL 4)**_.
  * Change Management Process:
    * **(1) Request for Change (RFC)**:
      * All proposed changes (new additions, modifications, or removals of IT services), must begin with a formal RFC.
      * Details the purpose of the change, its potential impact, and a plan for implementation and rollback.
      * Recorded and logged in to CMDB
      * Changes are categorized based on their risk and impact.
        * The three main types are:
          * **Standard Change**s: Low-risk, pre-approved, and repeatable changes, such as a routine software patch.
          * **Normal Changes**: Changes that require a formal review and approval process, often involving a Change Advisory Board (CAB). Examples include a major system upgrade.
          * **Emergency Changes**: Urgent changes needed to resolve a major incident or address a critical security vulnerability. These changes are expedited, with approval often occurring after the change is implemented.
    * **(2) Review The Change**:
      * A Change Manager, (often with help of others typically part of a Change Approval Board (CAB)) review and assess the change and associated documentation/details
      * impact, risks, and benefits of a proposed change are evaluated
      * ensures that the change aligns with business goals and that a proper back-out plan is in place in case of failure
    * **(3) Approve/Reject The Change**:
      * once the assessment/review is complete, the Change Manager and CAB team of experts then either approve or reject the change
      * the response is recorded in the CMDB (or change management documentation)
      * CAB team may require a rollback or backout plan for the change
    * **(4) Test The Change**:
      * once approved it should be tested in a controlled and isolated environment from production
      * ensures no interruption
    * **(5) Schedule and Implement The Change**:
      * change is scheduled so that it can be implemented with the least impact on the system and its customers
      * typically done in a "maintenance window", during off hours or non peak hours
      * testing should discover problems, but some unforeseen problems may occur, its important to have a rollback/backout plan to restore the previous state
    * **(6) Document the Change**:
      * ensures that all interested parties are aware of the change
      * often requires change in configuration management documentation
      * ensures that the system can return to a state before the change if required
      * after implementation, a _post-implementation review (PIR)_ is conducted to confirm that the change was successful and to identify any lessons learned for future improvements.




## 7.10 - Implement recovery strategies

* Backup storage strategies (e.g., cloud storage, onsite, offsite)
* Recovery site strategies (e.g., cold vs. hot, resource capacity agreements)
* Multiple processing sites
* System resilience, high availability (HA), Quality of Service (QoS), and fault tolerance


## 7.11 - Implement Disaster Recovery (DR) processes

* Response
* Personnel
* Communications (e.g., methods)
* Assessment
* Restoration
* Training and awareness
* Lessons learned

## 7.12 - Test Disaster Recovery Plans (DRP)

* Read-through/tabletop
* Walkthrough
* Simulation
* Parallel
* Full interruption
* Communications (e.g., stakeholders, test status, regulators)

## 7.13 - Participate in Business Continuity (BC) planning and exercises

## 7.14 - Implement and manage physical security

* Perimeter security controls
* Internal security controls

## 7.15 - Address personnel safety and security concerns

* Personnel Safety concerns are an essential element of security operations
* cant replace people
* **Duress**
  * type of system used when personnel are working alone
  * person can raise on alarm in case of an emergency (likely a button or switch)
  * this triggers and alert to a monitoring entity that will initiate a phone call or text message back to the individual who sent the distress call
  * often include code or phrase that personnel use to verify that everything is ok or if there is an actual problem
  * if the person indicates that there is a problem, emergency services will be notified and sent to the location
* **Travel**
  * safety concern due to criminals might target an organization's employees while they are traveling
  * training people on safe practices while traveling will enhance their safety and prevent security incidents
    * Verifying a person's identity before opening a hotel door or call the front desk to verify the person
  * Risks associated to electronic devices while traveling
    * **Sensitive Data**
      * ideally they should not contain any sensitive data (prevents loss)
      * if needed it should be protected with strong encryption
    * **Malware and Monitoring Devices**
      * both malware and physical monitoring devices have reported as being installed on individuals devices will in foreign countries
      * maintain physical control of devices at all times can prevent these attacks
      * recommended to bring temp devices instead, which can be reimaged/wiped clean after the trip
    * **Free Wi-Fi**
      * "on-path attack" / "man-in-the-middle"
      * can easily be a trap to capture all user's traffic
      * users should use their smartphone to create wifi connections (tethering or wifi hotspot)
    * **VPNs**
      * employees should have access to vpns so they can use them to create secure connections
      * used to access resources in the internal network (including work email)
* **Emergency Management**
  * plans/practices helps an organization address personnel safety and security after a disaster
    * disasters can be natural (floods, hurricanes, tornadoes, etc) or as a result of people's actions (fires, terrorist attack, or cyberattacks causing massive power outages)
  * different plans for each type of disaster they are likely to experience
  * safety of personnel is and should be a primary concern and consideration
* **Security Training and Awareness**
  * key in any InfoSec programs
  * should be easy to add personnel safety and security topics
  * ensure that personnel are aware of duress systems, travel best practices, emergency management plans, and general safety and security best practices
  * should also include comprehensive coverage of cybersecurity topics as well, which include
    * **_Insider Threat_**
      * educate employees on the risks associated with unauthorized access or misuse of company data by employees, contractors, or business partners
      * should highlight signs of potential insider threats and the protocols for reporting suspicious behavior
    * **Social Media Impacts**
      * should address risks and vulnerabilities associate with oversharing on social media platforms
      * teach them about social engineering attacks that leverage publicly available information and the importance of setting strict privacy settings
    * **Two-factor authentication (2FA) Fatigue**
      * address common issue where users become complacent or irritated with 2FA, often trying to bypass or minimize its use
      * training should emphasize the importance of 2FA in protecting both personal and organizational data
      * ways to make 2FA more user-friendly and the potential consequences of neglecting this security measure