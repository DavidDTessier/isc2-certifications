# Domain 8 - Software Development Security

## 8.1 - Understand and integrate security in the Software Development Life Cycle (SDLC)

* Development methodologies (e.g., Agile, Waterfall, DevOps, DevSecOps, Scaled Agile Framework)
* Maturity models (e.g., Capability Maturity Model (CMM), Software Assurance Maturity Model (SAMM))
* Operation and maintenance
* Change management
* Integrated Product Team

## 8.2 - Identify and apply security controls in software development ecosystems

* **Software Configuration Management (CM)**
  * **Versioning**
    * a labeling or numbering system that differentiates between different software sets and configurations across multiple machines or different points in time
    * example: first version is v1.0, first minor update version is v1.1, and after a major update the version is v2.0



* Programming languages
* Libraries
* Tool sets
* Integrated Development Environment
* Runtime
* Continuous Integration and Continuous Delivery (CI/CD)
* 
* Code repositories
* Application security testing (e.g., static application security testing (SAST), dynamic application security testing (DAST), software composition analysis, Interactive Application Security Test (IAST))

## 8.3 - Assess the effectiveness of software security

* Auditing and logging of changes
* Risk analysis and mitigation

## 8.4 - Assess security impact of acquired software

* Commercial-off-the-shelf (COTS)
* Open source
* Third-party
* Managed services (e.g., enterprise applications)

### Cloud Services

* assets that use cloud computing
* referred to as "managed services"
* Cloud computing is referred to on-demand access to computing resources available from anywhere
* Cloud computing resources are highly available and easily scalable
* typically leased from outside the organization, but could also be hosted on-premises within an organization
  * those hosted outside the org are typically outside the direct control of the org making managing risk more difficult
* some provide only data storage and access
  * org must ensure that security controls are in place to prevent unauthorized access to the data
* [DoD's Cloud Computing Security Requirements Guide (CC SRG)](https://www.schellman.com/blog/cloud-compliance/dod-cloud-computing-security-requirements)
  * defines specific requirements for U.S. government agencies to follow when evaluating the use of cloud computing assets
  * document identifies computing requirements for assets labeled _Secret_ and below using six separate levels which are as followed:
  * **_Impact Levels_**
    * **Impact Level 1 (IL1)**
      * Not used in current CC SRG
      * This level was for non-critical public information, with a security baseline focused on basic availability.
      * No longer used because this type of data, which is publicly available, doesn't require a specific DoD authorization.
    * **Impact Level 2 (IL2)**
      * Data Types:
        * Non-critical Unclassified Information, and unclassified information that is approved for public release
        * It includes some low-confidentiality information that requires minimal access control
      * Security Requirements:
        * The security controls are based on the FedRAMP Moderate baseline.
        * A compromise would have a limited adverse effect on DoD operations.
    * **Impact Level 3 (IL3)**:
      * Not used in current CC SRG
      * This level was for Controlled Unclassified Information (CUI).
      * It has been consolidated into IL4 to streamline the framework and avoid a redundant authorization level.
    * **Impact Level 4 (IL4)**:
      * Data Types:
        * Controlled Unclassified Information (CUI) and other non-critical mission information. 
        * It includes data such as "For Official Use Only" (FOUO), Personally Identifiable Information (PII), and Protected Health Information (PHI).
      * Security Requirements:
        * IL4 requires a higher level of security than IL2.
        * It builds upon the FedRAMP Moderate baseline with additional DoD-specific security controls. 
        * The loss of data at this level could result in a serious adverse effect on operations.
    * **Impact Level 5 (IL5)**:
      * Data Types:
        * Higher-Sensitivity CUI and Mission-Critical Information, and National Security Systems (NSS).
      * Security Requirements:
        * IL5 mandates more stringent security controls for confidentiality, integrity, and availability. The security baseline is built on the FedRAMP High baseline, with additional DoD-specific controls and a higher emphasis on availability and integrity. A compromise would have a severe or catastrophic adverse effect.
    * **Impact Level 6 (IL6)**:
      * Data Types:
        * Classified Information up to Secret.
        * Highest level
        * Security Requirements:
          * IL6 requires the most rigorous security measures.
          * The cloud infrastructure must be dedicated and physically isolated from other cloud tenants. 
          * It must be a DoD-owned or operated environment, and personnel must have the appropriate security clearances. 
          * This level's security controls are based on the FedRAMP High baseline and the [CNSSI 1253 Classified Information Overlay](https://www.dcsa.mil/portals/91/documents/ctp/nao/CNSSI_No1253.pdf).
  * all data (at rest and in transit) should be encrypted
  * customer should manage encryption, including controlling all encryption keys (not vendor managed keys)
    * reduces the risk of insider threat (at the vendor) and supports data destruction using cryptographic erasure methods
* **Shared Responsibility Models**
  * aka shared fate
  * varying levels of maintenance and security responsibilities for assets, depending on the service model
    * includes maintaining the assets, ensuring that they remain functional and keeping the systems and applications up-to-date with current patches
  ![Shared Resp Model](./images/share-resp-model.png)
  * **_Software as a Service (SaaS)_**
    * provides fully function enterprise applications accessible via web browser (Gmail)
    * vendor is responsible to all maintenance of the SaaS services
    * comes with share responsibilities for data and applications
    * customers may make configuration changes
    * customers share responsibility for keeping the data security at rest and in transmit (TLS)
  * **_Infrastructure as a Service (IaaS)_**
    * provides basic computing resources to customers
    * includes servers, storage, and networking resources
    * customers install OS's and applications and perform all required maintenance on the OS and applications
    * vendor maintains the cloud-based infrastructure (host), ensuring the customers have access to the leased systems
  * **_Platform as a Service (PaaS)_**
    * provides consumers with a computing platform
      * including hardware, OS, and a runtime environment
    * runtime environment includes programming languages, libraries, services, and other tools tools supported by the vendor
    * customers deploy, manage, and modify applications and configurations settings on the host
    * vendor is responsible for maintenance of the host and the underlying cloud infra
* **NIST Publications**
  * [NIST SP 800-144 - Guidelines on Security and Privacy in Public Cloud Computing](https://csrc.nist.gov/pubs/sp/800/144/final)
    * provides in-depth analysis on security issues and guidance related to computing
  * [NIST SP 800-145 - The NIST Definition of Cloud Computing](https://csrc.nist.gov/pubs/sp/800/145/final)
    * provides standard definitions for many cloud-based services
    * includes definitions for service models (SaaS, IaaS, PaaS) and deployment model definitions (public, private, community, and hybrid)
* **Deployment Models**
  * **_Public Cloud_**
    * model includes assets available for any consumers to rent or lease and is hosted by an external CSP/vendor
    * service level agreement can effectively ensure that the CSP provides the cloud-based services at a level acceptable to the organization
    * customers and csp's have a shared responsibility/share fate
    * maintenance requirements are typically split based on the service model (SaaS, PaaS, IaaS)
  * **_Private Cloud_**
    * model is used for cloud-based assets for a single organization
    * org can create and host private clouds using their own on-premises resources
    * org is responsible for any and all maintenance
    * org can also rent resources from a third-party for exclusive use of their org
      * maintenance requirements are typically split based on the service model (SaaS, PaaS, IaaS)
  * **_Community Cloud_**
    * provides cloud-based assets to two or more organizations that have a shared concern
      * such as a similar mission, security requirements, policy, or compliance considerations
    * assets can be owned/managed by one or more of the organizations
    * maintenance responsibilities are share based on who is hosting the assets and the service models in use
  * **_Hybrid Cloud_**
    * includes a combination of two or more clouds that are bound together by a technology that provides data and application portability
    * maintenance responsibilities are share based on who is hosting the assets and the service models in use
* **Managed Security Service Provider (MSSP)**
  * third-party (often cloud-based) services that provide remote oversight and management of on-prem IT or Cloud IT
  * some are general purpose or focused on specific IT area (security, etc)
  * some are vertical focused also (legal, medical, fin, gov, etc)
  * _Security-as-a-Service (SECaaS)_
    * various forms of security solutions/services being offered through cloud solutions
    * SIEM/SOAR, MDR/XDR, IDS/IPS, etc
* **Rapid Elasticity and Scalability**
  * Elasticity
    * ability of a system to **automatically expand and contract rapidly**
    * Closely related to Scalability
    * Scale-in / Scale-out capacity on demand
  * Scalability
    * ability of a system to handle growth of users or work
    * Ability to grow as demand increases
    * requires system shutdonw
    * Two types:
      * Horizontal
        * Adding more services to the pool to meet deman
          * More VMs, pods, etc
          * Load balancing plays a part in this mechanism to distribute load
      * Vertical
        * Adding more resources (CPU, RAM, Storage,etc) to existing resources (i.e. VMs)
* [**Software-Defined Data Center (SDDC)**](https://en.wikipedia.org/wiki/Software-defined_data_center)
  * aka _Services integration_, _Cloud integration_, systems integration_, and _integration platform_
  * design and architecture of an IT/IS solution that stitches together elements from on-premises and cloud sources into a seamless productive environment
  * goals of service integration are to eliminate data silos, expand access, claify processing visibility, and improve functional connectivity of on-site and off-site resources
  * include Software-Defined Networking, Software-Defined Storage, computing resources, and management/automation processes
* **Serverless Architecture**
  * cloud computing concept where code is managed by the customer and the platform or server is managed by the CSP/Vendor
  * physical server runs the code, but the execution model allows the software designer/developer/architect to focus on the logic and the hosting is abstracted away
  * aka _Function-as-a-Service (FaaS)_
  * typically triggered and run until completed

## 8.5 - Define and apply secure coding guidelines and standards

* Security weaknesses and vulnerabilities at the source-code level
* Security of application programming interfaces (API)
* Secure coding practices
* Software-defined security
