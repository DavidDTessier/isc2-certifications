![Domain 4](images/domain4.png)

## 4.1 Advocate training and awareness of application security

Cloud Development Basics
* Security By Design
    * declares security should be present throughout every step of the process
    * various models exist to help, like [Building Security In Maturity Model (BSIMM)](https://owasp.org/www-pdf-archive/Bsimm09.pdf)
    * Pairs well with DevSecOps
* Shared Security Responsibility
    * security is the resposibility for everyone from the most junior memeber of the team to senior management
    * primary principle of DevSecOps
* Security as a Business Objective
    * Risk management through security controls should be a key business objective, similar to customers satisfaction or revenue
    * requires org-wide security awareness and commitment

Common Pitfalls
* Performance
    * cloud software development often relies on loosely coupled services
    * makes designing for and meeting performance goals more complex as multiple components may interact in unexpected ways
    * TEST end-2-end and stress testing
    * eventual consistency
        * optimistic replication
        * key to distributed systems
        * 
    * strong consistency
        * data must be strongly persisted and available on all system nodes
        * ACID transactions
* Scalability
    * key feature of the cloud is the ability to scale allowing applications and services to grow and shink on demand
    * requires developers to think about how to retain state acrosss instances and handle faults with individual servers
    * scale out is better than scale up 
* Interoperability
    * work accros multiple platofrms, services, systems
    * very important espcially with multi-vendor and multi-cloud scenarios
* Portablitiy
    * design software that can move between on-prem and cloud or between cloud providers
    * containerization
    * making ssystems agnostic is complex .. may need to make compromises
* API Security
    * consideratoins
        * access control
        * data encrytion
        * throtteling
        * rate limiting
    * CSP offer PaaS services
        * Azure API management
        * GCP APi gateway/Apigee

Common cloud vulnerabilities (e.g., Open Web Application Security Project (OWASP) Top-10, SANS Top-25)

## 4.2 Describe the Secure Software Development Life Cycle (SDLC) process

» Business requirements
» Phases and methodologies (e.g., design, code, test, maintain, waterfall vs. agile)

## 4.3 Apply the Secure Software Development Life Cycle (SDLC)

» Cloud-specific risks

» Threat modeling (e.g., Spoofing, Tampering,
Repudiation, Information Disclosure, Denial of
Service, and Elevation of Privilege (STRIDE),
Damage, Reproducibility, Exploitability, Affected
Users, and Discoverability (DREAD), Architecture,
Threats, Attack Surfaces, and Mitigations
(ATASM), Process for Attack Simulation and
Threat Analysis (PASTA))

» Avoid common vulnerabilities during
development

» Secure coding (e.g., Open Web Application
Security Project (OWASP) Application Security
Verification Standard (ASVS), Software Assurance
Forum for Excellence in Code (SAFECode))

» Software configuration management and
versioning

## 4.4 Apply cloud software assurance validation

» Functional and non-functional testing
» Security testing methodologies (e.g., blackbox, whitebox, static, dynamic, Software Composition Analysis
(SCA), interactive application security testing (IAST))
» Quality assurance (QA)
» Abuse case testing

## 4.5 Use verified secure software

» Securing application programming interfaces (API)
» Supply-chain management (e.g., vendor assessment)
» Third-party software management (e.g., licensing)
» Validated open-source software

## 4.6 Comprehend the specifics of cloud application architecture

» Supplemental security components (e.g., web application firewall (WAF), Database Activity Monitoring (DAM),
Extensible Markup Language (XML) firewalls, application programming interface (API) gateway)
» Cryptography
» Sandboxing
» Application virtualization and orchestration (e.g., microservices, containers)

## 4.7 Design appropriate identity and access management (IAM) solutions

» Federated identity
» Identity providers (IdP)
» Single sign-on (SSO)
» Multi-factor authentication (MFA)
» Cloud access security broker (CASB)
» Secrets management
