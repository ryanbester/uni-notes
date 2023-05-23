---
title: "2. Access Control"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 2. Access Control

[🔒 Recording](https://github.com/ryanbester/uni-resources/tree/main/ccc/y1/security/2-access-control)

## Identification and Authentication

- Users must be identified to enable:
    - user-specific access controls
    - individual accountability for their actions
- Claimed identities must be authenticated
    - First line of defence for the system
    - Safeguards against unauthorised use (internal and external)
    - Traditional passwords are the most common means of authentication in digital systems
        - **Pro**: Conceptually simple for designers and users can provide good protection if used correctly
        - **Con**: Protection is often compromised by users

### Password Weaknesses (Vulnerabilities)

- Badly selecgted, e.g. too short, dictionary words, personal data
- Written down
- Infrequently (or never) changed
- The same for multiple systems
- Only required at the start of a session
- Forget them
- Share them

### Confidentiality vs Availability

A traditional defence against password guessing is to add a lock out after three failed password attempts.

This, however, could enable a form of DoS attack since the attacker could deliberately lock out users.

### NCSC Password Guidance

NCSC encourages organisations to reduce reliance on users' recall of large numbers of complex passwords, here are 6 tips:

1. Reduce your organisation's reliance on passwords
2. Implement technical solutions
3. Protect all passwords
4. Help users cope with password overload
5. Help users to generate better passwords
6. Use training to support key messages

## Access Control Fundamentals

- **Identity**: The properties of an individual or resource that can be used to identify uniquely one individual or resource
- **Authentication**: Ensuring that the identity of a subject or resource is the one claimed
- **Authorisation**: The process of checking the authentication of an individual or resource to establish their authorised use of, or access to, information or other assets
- **Accouting**: Ensures that user activities can be tracked back to them
- **Audit**: Formal or informal review of actions, processes, policies, and procedures
- **Compliance**: Working in accordance with the actions, processes, policies, and procedures laid down necessarily having independent reviews

## Factors of Authentication

- Something a supplicant knows:
    - PIN
    - password
    - passphrase
    - security questions/answers
- Something a supplicant has:
    - dumb cards (magnetic stripe ID cards and ATM cards)
    - smart cards (Chip & PIN cards)
    - security token
- Something a supplicant is:
    - fingerprint
    - palmprint
    - retina/iris scan
    - voice
    - keyboard kinetic measurements

### Strong Authentication

Strong customer authentication is a procedure based on the use of two or more of the previous factors.

The elements selected must be mutually independent, i.e. the breach of one does not compromise the others.

### Biometric System Requirements

- **Universality**: Every individual in the target population should possess the trait
- **Distinctiveness**: Ability of the trait to sufficiently differentiate between any two persons
- **Persistence**: The trait should be sufficiently invariant over a period of time
- **Collectability**: The trait should be easily obtainable
- **Performance**: High recognition accuracy and speed should be achievable with limited resources in a variety of operational and environmental conditions
- **Acceptability**: The biometric identifier should have a wide public acceptance and the device used for measurement should be harmless
- **Circumvention**: Spoofing of the characteristic using fraudulent methods should be difficult

### Effectiveness of Biometrics

Biometric technologies are evaluated bsed on three basic criteria:

- **False Reject Rate (FRR)**: The percentage of identification instances in which authorised users are denied access
- **False Accept Rate (FAR)**: The percentage of identification instances in which unauthorised users are allowed access
- **Crossover Error Rate (CER)**: The level at which the number of false rejections equals the false acceptances

![Effectiveness of Biometrics](/img/cyber-security/y1/far-frr-relationship.png)

## Access Control Policies

Access privileges are specified and subjects' access to objects are determined through a security policy.

- **DAC**: Discretionary access control policy: controls access based upon identity
- **MAC**: Mandatory access control policy: controls access based upon security labels
- **RBAC**: Role-based access control policy: controls access based upon roles
- **ABAC**: Attribute-based access control policy: control access based upon attributes

File systems usually have read, write, and execute permissions.

### Privileged Access

- System or application administrator
- Sysadmins can:
    - Enroll new users
    - Modify user access rights
    - Remove user access rights
- Could also modify groups or levels of privileges, rebuild the system, erase data, grant or deny access to applications, change passwords, and even alter or destroy event logging or auditing data
- These accounts have great power and wide-ranging capabilities and their use must be tightly controlled and safeguarded
- Their potential to disrupt operations, accidental or otherwise, is enormous

### Discretionary Access Control (DAC)

- At the discretion of the owner
- Often provided using an access matrix

### Mandatory Access Control (MAC)

- Less individual freedom, with the OS having overall control
- Rules for defining how a subject can behave
- Uses sensitivity (or security) labels

#### Access Control Models

- **Bell-LaPadula Confidentiality Model**:
    - No read up, no write down
- **Biba Integrity Model**:
    - No write up, no read down
- **Clark-Wilson Integrity Model**:
    - No changes by unauthorised subjects
    - No unauthorised changes by authorised subjects
    - Maintenance of internal and external consistency
        - Internal consistency: system does what is expected to do without exception
        - External consistency: data in the system is consistent with similar data in the outside world
- **Graham-Denning Access Control Model**:
    - Objects, subjects, and rights
- **Brewer-Nash Model**:
    - Subjects can access only one of two conflicting sets of data, prevents conflicts of interest

### Role-Based Access Control (RBAC)

- Newer than DAC and MAC
- Centrally administered set of controls
- Assigning permissions based upon roles
- Users who perform a similar function are grouped together
- Useful model for companies with high employee turnovers

### Attribute-Based Access Control (ABAC)

- Generalises access control based on the 'role' attribute of users, to various other attributes of the users, environment, and information assets
