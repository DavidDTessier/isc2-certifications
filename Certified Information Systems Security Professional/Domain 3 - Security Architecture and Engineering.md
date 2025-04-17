# Domain 3 - Security Architecture and Engineering

## 3.1 - Research, implement and manage engineering processes using secure design principles

### Threat Modeling

* process where potential threats are identified, categorized, and analyzed.
* can be performed proactive during design and development or as a reactive measure once a product has been deployed
* process identifies
  * the potential harm,
  * the probability of occurrence,
  * the priority of concern,
  * the means to eradicate or reduce the threat
* not meant to be a single event but initiated early in the design process and continue throughout a systems lifecycle
* proactive (during design and build) vs reactive (post-deployment, pen testing, threat hunting)
* Microsoft uses a [Security Development lifecycle (SDL)](https://www.microsoft.com/en-us/securityengineering/sdl)
  * includes a range of procedures aim at bolstering security assurance and compliance prerequisites.
  * follows the [NIST Secure Software Development Framework](https://csrc.nist.gov/Projects/ssdf) closely
  * aids developers in creating secure software by diminishing the quantity and seriousness of software vulnerabilities while trimming development expenses
* Modelling Frameworks
  * **STRIDE**
    * https://en.wikipedia.org/wiki/STRIDE_model
    * Developed by Microsoft as a threat categorization scheme
    * stands for :
      * **_Spoofing_**
        * an attack with the goal of gaining access to a target system through the use of falsified identity.
        * an attacker spooks their identity as a valid or authorized entity, they are often able to bypass filters and blockades against unauthorized access
      * **_Tampering_**
        * an action resulting in unauthorized changes or manipulation of data, whether in transit or at rest.
      * **_Repudiation_**
        * ability of a user or attacker to deny having performed an action or activity using plausible deniability
        * attacks can also result in innocent third parties being blamed 
      * **_Information Disclosure_**
        * revelation or distribution of private, confidential, or controlled information to external or unauthorized entities
      * **_Denial of service (DoS)_**
        * attack that attempts to prevent
      * **_Elevation of privilege_**
    * **Process for Attack Simulation and Threat Analysis (PASTA)**
      * https://www.iriusrisk.com/resources-blog/pasta-threat-modeling-methodologies
      * a seven-stage threat modelling methodology.
      * risk-centric approach that aims at selecting or developing countermeasures in relation to the value of the assets to be protected.
      * Seven-Steps:
        * **Stage I: Definition of the Objectives (DO)**
        * **Stage II: Definition of the Technical Scope (DTS)**
        * **Stage III: Application Decomposition and Analysis (ADA)**
        * **Stage IV: Threat Analysis (TA)**
        * **Stage V: Weakness and Vulnerability Analysis (WVA)**
        * **Stage VI: Attack Modelling & Simulation (AMS)**
        * **Stage VII: Risk Analysis & Management (RAM)**
    * **Visual, Agile, and Simple Threat (VAST)**
      * https://smartstatetech.medium.com/threat-modeling-methodology-vast-5c7de64cd924
      * Threat modelling concept that integrates threat and risk management in to an Agile programming environment on a scalable basis
      * two types of models
        * VAST: Application Threat Models
          * [App Threat Models](https://www.threatmodeler.com/application-threat-modeling-guide-for-cisos/) for dev teams are created using [process flow diagrams (PFD)](https://www.threatmodeler.com/2017/09/18/architecturally-based-process-flow-diagrams/).
            * PFD's map the features and communications of an application in much the same way developers and architects think about the application during an SDLC design session
        * VAST: Operational Threat Models
          * designed for the infra teams
          * more similar to traditional Data Flow Diagrams (DFDs) than app threat models, the data flow information is presented from an attacker - not a data packet - perspective, by relying on PFDs instead

* Least privilege

### Defense in Depth

* also known as _layering_ 
* https://en.wikipedia.org/wiki/Defense_in_depth_(computing)
* also known as the [onion model](https://en.wikipedia.org/wiki/Onion_model)
* use of multiple overlapping controls in a series for one objective
* no one control can protect against all possible threats
* a single failed control **SHOULD NOT** result in the exposure of systems and/or data
* a serial configurations are very narrow but deep
* a parallel configuration are very wide but shallow, useful in distributing computing applications
* _Defense in breadth_ or _Diversity in defense_
  * Using a wide range of security products from varied vendors significantly reduces or avoids the risk of a single exploit compromising several layers at once.
  * Can be problematic if elements of the security layers are from the same vendor or share common code , since a vulnerability could affect numerous layers simultaneously

* Secure defaults
* Fail securely
* Segregation of Duties (SoD)
* Keep it simple and small
* Zero trust or trust but verify
* Privacy by design
* Shared responsibility
* Secure access service edge

## 3.2 - Understand the fundamental concepts of security models (e.g., Biba, Star Model, Bell-LaPadula)

## 3.3 - Select controls based upon systems security requirements

## 3.4 - Understand security capabilities of Information Systems (IS) (e.g., memory protection, Trusted Platform Module (TPM), encryption/decryption)

## 3.5 - Assess and mitigate the vulnerabilities of security architectures, designs, and solution elements

* Client-based systems
* Server-based systems
* Database systems
* Cryptographic systems
* Industrial Control Systems (ICS)
* Cloud-based systems (e.g., Software as a Service (SaaS), Infrastructure as a Service (IaaS), Platform as a Service (PaaS))
* Distributed systems
* Internet of Things (IoT)
* Microservices (e.g., application programming interface (API))
* Containerization
* Serverless
* Embedded systems
* High-Performance Computing systems
* Edge computing systems
* Virtualized systems

## 3.6 - Select and determine cryptographic solutions

* Cryptographic life cycle (e.g., keys, algorithm selection)
* Cryptographic methods (e.g., symmetric, asymmetric, elliptic curves, quantum)
* Public key infrastructure (PKI) (e.g., quantum key distribution)

## 3.7 - Understand methods of cryptanalytic attacks

* Brute force
* Ciphertext only
* Known plaintext
* Frequency analysis
* Chosen ciphertext
* Implementation attacks
* Side-channel
* Fault injection
* Timing
* Man-in-the-Middle (MITM)
* Pass the hash
* Kerberos exploitation
* Ransomware

## 3.8 - Apply security principles to site and facility design

## 3.9 - Design site and facility security controls

* Wiring closets/intermediate distribution facilities
* Server rooms/data centers
* Media storage facilities
* Evidence storage
* Restricted and work area security
* Utilities and Heating, Ventilation, and Air Conditioning (HVAC)
* Environmental issues (e.g., natural disasters, man-made)
* Fire prevention, detection, and suppression
* Power (e.g., redundant, backup)

## 3.10 - Manage the information system lifecycle

* Stakeholders needs and requirements
* Requirements analysis
* Architectural design
* Development /implementation
* Integration
* Verification and validation
* Transition/deployment
* Operations and maintenance/sustainment
* Retirement/disposal