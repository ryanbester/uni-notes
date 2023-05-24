---
title: "5. Common Software Errors"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 5. Common Software Errors

[🔒 Recording](https://github.com/ryanbester/uni-resources/tree/main/ccc/y1/security/5-common-software-errors)

## Web Application Security Risks

Attack vectors may exist through your web app, each representing a risk.

![Web Application Security Risks](/img/ccc/y1/security/web-app-risks.png)

- Paths may be trivial to find/exploit, but may otherwise be very difficult
- The impact of each may be inconsequential to catastrophic
- Risks combine a likelihood associated with a threat agent, attack vector, and security weakness with the estimated technical/business impact

## Security Requirement Specification

The security requirement must be part of the overall statement of requirements document from which the design is generated.

Adding them later will add complexity and cost to any project.

Security should not be thought of as the need to defend against improper access and misuse. It also means:

- defensive coding to make sure that only valid and accurate data is processed by the system
- proper functional testing to ensure it behaves as expected and within the design criteria
- methods to back up and secure data against loss or damage
- adequate assurance of availability
- compliance with any legal and regulatory requirements
- security communicates
- effective auditing of activity

## Common Software Errors

The **Common Weakness Enumeration (CWE)** is a community-driven project maintained by MITRE, and contains a list of software security vulnerabilities.

Each vulnerability is listed with a description and mitigation.

MITRE partnered with SANS Institute to develop CWE/25. CWE/25 lists the 25 most critical software vulnerabilities.

A similar list is provided in the OWASP Top 10 Project. Both lists share many of the same vulnerabilities.

### Cross-Site Scripting (XSS)

XSS is improper neutralisation of input during web page generation.

XSS vulnerabilities occur when:

- Untrusted data enters a web app
- The web app dynamically generates a web page containing untrusted data
- On page generation, the app does not prevent entry of executable data, e.g. JavaScript, HTML tags, mouse events, etc
- Victim visits generated web page via browser, containing the script injected using the untrusted data
- Since script is from page sent by the web server, the victim's browser executes in the context of the web server's domain
- This violates the same-origin policy, scripts in one domain are not to access resources or run code in a different domain

Types of XSS:

- **Type 1: Reflected XSS (or Non-Persistent)**: The server reflects data in the HTTP request back in the HTTP response. The attacker makes victim supply bad content to the vulnerable web app, which is reflected back and executed by the victim's browser.
- **Type 2: Stored XSS (or Persistent)**: The app stores bad data in a database, message forum, visitor log, or other trusted data source. The dangerous data is later read back into the application and included in dynamic content.

#### XSS Preventation

Preventing XSS requires separation of untrusted data from active browser content.

- **Rule 0**: Never insert untrusted data except in allowed locations
- **Rule 1**: HTML escape before inserting untrusted data into HTML element content
- **Rule 2**: Attribute escape before inserting untrusted dat into HTML common attributes
- **Rule 3**: JavaScript escape before inserting untrusted data into JavaScript data values
- **Rule 3.1**: HTML escape JSON values in an HTML context and read the data with JSON.parse
- **Rule 4**: CSS escape and strictly validate before inserting untrusted data into HTML style property values
- **Rule 5**: URL escape before inserting untrusted data into HTML URL parameter values
- **Rule 6**: Sanitize HTML markup with a library designed for the job
- **Rule 7**: Avoid JavaScript URLs
- **Rule 8**: Prevent DOM-based XSS
- **Bonus 1**: Use HTTPOnly cookie flag
- **Bonus 2**: Implement content security policy
- **Bonus 3**: Use an auto-escaping template system
- **Bonus 4**: Use the X-XSS-Protection response header
- **Bonus 5**: Properly use modern JS frameworks

### SQL Injection

*"The software constructs all or part of an SQL command using externally-influenced input from an upstream component, but it does not neutralize or incorrectly neutralizes special elements that could modify the intended SQL command when it is sent to a downstream component."* - [Mitre CWE-89](https://cwe.mitre.org/data/definitions/89.html)

## Secure Development and Deployment

- Secure development is everyone's concern
- Keep your security knowledge sharp
- Produce clean, maintainable code
- Protect your code repository
- Secure the build and deployment pipeline
- Continually test your security
- Plan for security flaws
- Secure your development environment

### Securing the Development Environment

- Separate business and development functions
- Consider your development environment compromised
- Trust your developers, verify their actions
- The ISO 27000 series requires that live and development systems are kept separate
- User training may also be safer to run in a non-live system
- Functionality and acceptance testing is required before releasing to a production system

### Acceptance Processes

Security testing needs to consider:

- effectiveness of defensive coding
- protection against malware and code injection through interfaces
- backup and recovery of data
- access control
- auditing and behavioural analysis
- communications security
- resilience

### Change Control and Escrow

Any change to software risks introducting new bugs/vulnerabilities. Formal change control processes manage these risks.

- **Separation of duties** ensures the person responsible for testing the code isn't also responsible for its implementation
- **Two person control** requires that an additional person signs off on the code changes, to reduce accidental or malicious flaws
- **Version Control Systems** such as git and svn

### Patching

- Every software application and operating system contains bugs
- Code complexity and size makes it impossible to test 100% of execution paths
- Bugs have varied impacts on confidentiality, integrity, and availability
- Once found and fixed, suppliers issue a patch that can be installed on order to remove the vulnerability
- Patches should be rolled out at the earliest opportunity
    - Vulnerability may already be known to and exploited by attackers
    - Attackers may also try to reverse engineer patches to create new exploits
- But patches should be tested before roll out, in a non-live environment

### Accreditation and certification

**Certification** is a provision by an independent body of written assurance (a certificate) that the product, service, or system in question meets specified requirements.

**Accreditation** refers to formal recognition by an independent body generally known as an accreditation body, that a certification body operates according to international standards.

- Accredited certification typically mandated for safety/security critical systems
- Formal review process to approve information security architecture, policy, and procedures before the new/updated product/service/system is deployed/used
- Will typically require periodic review and re-accreditation
