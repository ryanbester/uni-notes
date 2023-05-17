---
title: "1.18. Authentication"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1.18. Authentication

## Authentication Methods

There are three main approaches to authentication:

- Something the user **knows** (e.g. passwords and PINs)
- Something the user **has** (e.g. a card or token)
- Something the user **is** (e.g. a biometric)

## Traditional Passwords

- A password is the most commonly used means of authentication in digital systems
- Advantages:
    - Conceptually simple for designers and users
    - Can provide good protection if used correctly
- Disadvantages:
    - Protection is often compromised by users

### Bad Password Behaviour

- Badly selected, e.g. too short, dictionary words, personal data
- Written down
- Infrequently changed
- The same for multiple systems
- Share them
- Forget them
- Only required at the start of a session

### Attacking Passwords

- Shoulder surfing
- Phising
- Keylogger attack
- Password cracking

### Improving Password Ssytems

- Educating users with better password practice
    - Using stronger passwords
    - Identifying phishing attacks
    - Not reusing passwords
- From system administrator's perspective:
    - Password filtering - password blacklists
    - Throttle login attempts

### Current Password Guidance

National Cyber Security Centre (NCSC) recommends using three random words as a password. This is:

- Generally longer than most normal passwords
- Self explanatory and easy to follow
- Combinations are more likely to new passwords
- Easy for users to remember

Passwords should never be stored in plaintext and should be salted and hashed.

### Salts

A salt is a large, random value used to randomise the output of a password hash.

Problems with salts:

- **Salt reuse**: If every use has the same salt added then security is substantially reduced if any one user's password is cracked.
- **Short salts**: Short salts are insufficient to increase password security

## Token-based Authentication

- Based upon possession of a physical identifier
- Could be software based or hardware based
- Examples:
    - Smart cards (e.g. Chip and PIN, contactless)
    - Code generators (e.g. HSBC's Secure Key)
    - Phone Apps
- Often combined with secret knowledge to form a 2-stage authentication
- Advantages:
    - An attacker must counterfeit or steal a token before gaining access
    - Illegal possession of a token can be used as evidence
    - Users cannot (easily) share their access privileges
    - Increased awareness of likely compromise
- Disadvantages:
    - Users always need to carry the token with them
    - Tokens can still be lost, stolen, run out of battery
    - Could be expensive to implement
    - May require some amount of user training

## Biometric Authentication

- Uses a user's physical characteristics or bahavioural traits
- Common biometric markers:
    - Retina scan
    - Fingerprint
    - Voice print
    - Signature dynamics
    - Face

## Error Rates

**False Acceptance Rate (FAR)** is the probability that a biometric system incorrectly matches a biometric sample with a non-matching template.
**False Rejection Rate (FRR)** is the probability that a biometric system fails to match a user's sample with a matching template.

![FAR/FRR Relationship](/img/cyber-security/y1/far-frr-relationship.png)
