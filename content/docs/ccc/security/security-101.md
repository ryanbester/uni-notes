---
title: "1. Security 101"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1. Security 101

[🔒 Recording](https://github.com/ryanbester/uni-resources/tree/main/ccc/y1/security/1-security-101)

## Information Security

**Information Security** is the preservation of confidentiality, integrity and availability of information.

- **Confidentiality**: Information is not disclosed to unauthorised individuals, entities, or processes
- **Integrity**: The accuracy and completeness of assets is safeguarded
- **Availability**: Information is accessible and usable upon demand by an authorised entity

***Confidentiality can impact Availability***: Users might find the lag due to disk-encryption a nuisance whereas the company is more concerned about the loss of data stored on the laptop in case of theft.

***Availability can impact Integrity***: Duplicating data to help ensure availability of data can mean that it is more difficult to guarantee its integrity, data will need to be updated in multiple locations to ensure consistency.

***Integrity can impact Confidentiality***: Repeating given credit card details during phone purchases ensures integrity but unauthorised individuals may overhear this info.

***Availiability can impact Confidentiality***: Taking a compromised system offline in immediate response to a data breach to mitigate consequence.

## Essential Terminology

- **Asset**: Anything that has value to the organisation, its business operations, and its continuity
- **Threat**: A potential cause of an incident that may result in harm to a system or organisation
- **Vulnerability**: A weakness of an asset or group of assets that can be exploited by one or more threats
- **Impact**: The result of an information security incident, caused by a threat, which affects assets
- **Risk**: The potential that a given threat will exploit vulnerabilities of an asset or group of assets and thereby cause harm to the organisation

These can be defined with a umbrella in rain analogy.

- **Asset**: The person holding the umbrella
- **Threat**: Rain falling from the sky
- **Vulnerability**: Without an umbrella, the threat of rain could have an impact on the asset
- **Impact**: The person getting wet
- **Risk**: The choice of going outside in the rain

## Assets

- **Primary Assets**:
    - Business processes and activities
    - Information
- **Supporting Assets** (on which the primary assets rely):
    - Hardware
    - Software
    - Network
    - Personnel
    - Site
    - Organisation's structure

### Business Processes

- Process that contain secret processes or processes involving proprietary technology
- Processes that, if modified, can greatly affect the accomplishment of the organisation's mission
- Processes that are necessary for the organisation to comply with contractual, legal, or regulatory requirements

Business processes/procedures (i.e. documented instructions to accomplish a certain task) are often overlooked. They are information assets in their own right.

### Information

- **Business critical information** for the exercise of the organisation's mission
- **Personal information**, as can be defined specifically in the sense of the national laws regarding privacy
- **Strategic information** required for achieving objectives determined by the strategic orientations
- **High-cost information** whose gathering, storage, processing, and transmission require a long time and/or involve a high acquisition cost

### Hardware

This is the physical technology that:

- houses and executes the software
- stores and carries the data
- provides the interface for data entry/removal from the system

Traditional physical security, like locks and keys, restrict access to and the interaction with the hardware components.

Securing the physical location of the hardware is important as physical access may mean information can be extracted.

Remember, the hardware itself may be cheap but the information stored on it may be worth millions.

### Software

The software component of Information Security comprises:

- applications
- operating systems
- assorted command utilities

Can be considered the most difficult IS component to secure.

Unfortunately, software development is often under-resourced, so information security is usually added as an afterthought rather than being embedded as an integral part.

The exploitation of software errors in software programming accounts for a substantial proportion of attacks on information.

### Networks

This was the component that increased the need for information security; challenges emerge as IS systems are increasingly interconnected.

- Manage the network perimeter
    - Use firewalls
    - Prevent malicious content
- Protect the internal network
    - Segregate network
    - Secure wireless access
    - Enable secure administration
    - Configure the exception handling process
    - Monitor the network
    - Assurance processes

### Personnel

Often overlooked; people always make mistakes, fall victim to social engineering, and may be susceptible to bribery/blackmail.

- Produce a user security policy
- Establish a staff induction process
- Maintain user awareness of the security risks faced by the organisation
- Support the formal assessment of security skills
- Monitor the effectiveness of security training
- Promote an incident reporting culture
- Establish a formal disciplinary process

## Implications

How might the compromise of an information asset affect supporting assets and vice versa?

- Leaking your access code might allow an unauthorised person to get access to a company's secure area
- Losing data centre due to fire may result in destruction of all information assets unless backed-up off-site
- Stolen laptop may result in third-party accessing trade secrets
- Leaking your password for your internet bank may result in monetary loss

## Subjects and Objects of an Attack

Assets may be either the subject or object of an attack

- **Subject**: An active tool used to conduct an attack
- **Object**: The entity being attacked

## Information Security Governance

Refers to *"how organisations control, direct & communicate their cyber security risk mangement activities"* - NCSC

For example, policies must be managed as they constantly change.

To remain viable, security policies must have:

- An individual responsible for the policy (policy adminstrator)
- A schedule of reviews
- A Method for making recommendations for reviews
- A specific policy issuance and revision date

## Policies, Standards, Guidelines, and Procedures

- **Policy**: A principle or rule to guide decisions and achieve rational outcomes
- **Standards**: Detailed statements, quantifying what must be done to comply with a policy
- **Guideline**: A set of recommended actions to assist in complying with a policy
- **Procedure**: A list of steps that constitute instructions for performing some action or accomplishing some task

### Disseminating Policies

Policies should be promoted/supported by a security education, training, and awareness (SETA) programme that helps employees do their jobs securely.

- **Education**:
    - Not everyone needs a formal degree or certificate in information security
    - But some roles may require certain employees to hold/attain information security academic qualifications or industry certification
- **Training**:
    - EVERYONE in an organisation needs to be trained and aware of information security
    - Provides employees with hands-on instruction and detailed information designed to prepare them to perform duties securely
    - Management of information security can develop customised in-house training or outsource training
- **Awareness**:
    - Keeps information security at forefront of the user's mind
    - Can be as simple as security posters, newsletters, flyers, etc
    - May include printed mouse-pads or company mugs

### NCSC Guidance

Good security governance should:

- Clearly link security activities to your organisation's goals and priorities 
- Identify the individuals, at all levels, who are responsible for making security decisions and empower them to do so
- Ensure accountability for decisions
- Ensure that feedback is provided to decision-makers on the impact of their choices
- Fit into an organisation's wider approach to governance. Security needs to be considered alongside other business priorities, such as health and safety, or financial governance.

## Incidents Happen

Preventive activities based on the results of risk assessments can lower the number of incidents, but not all incidents can be prevented.

An incident response capability is therefore necessary for:

- rapidly detecting incidents
- minimising loss and destruction
- mitigating the weaknesses that were exploited
- restoring IT services
