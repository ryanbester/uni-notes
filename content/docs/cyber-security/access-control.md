---
title: "1.10. Access Control"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1.10. Access Control

## Basic Elements

Access Control has three basic elements:

- A **Subject** is an entity that is capable of accessing objects, such as users and applications
- An **Object** is a resource to which access is controlled, such as files and applications
- An **Access right** describes the way a subject may access an object, such as read, write, execute, delete, etc

## Access Control Policies

An **access control policy** determines how a subject can access an object and how the privileges are specified.

These include:

- **Discretionary Access Control (DAC)**: Controls access based upon **identity**
- **Mandatory Access Control (MAC)**: Controls access based upon **security labels**
- **Role-based Access Control (RBAC)**: Controls access based on **roles**

### Discretionary Access Control

Access is granted at the discretion of the owner.

Can be represented as an Access Matrix, ACL, or C-List.

#### Access Matrix

- One dimension contains subjects
- Other dimension lists the objects
- Each entry indicates the access rights of a particular object for a particular subject

![Access Matrix](/img/cyber-security/y1/access-matrix.png)

#### Access Control List (ACL)

- Stores all the access rights to an object with the **object**
- Represents a column in the access control matrix

![Access Control List](/img/cyber-security/y1/acl.png)

#### Capability List (CL or C-List)

- Stores all the access rights to an object with the **subject**
- Represents a row in the access control matrix

![Compatibility List](/img/cyber-security/y1/c-list.png)

### Mandatory Access Control

There is less individiual freedom with a MAC, with the OS having overall control.

There are rules for defining how each subject can behave.

Uses sensitivity, or security, labels.

![MAC Security Labels](/img/cyber-security/y1/mac-security-labels.png)

#### Bell LaPadula (BLP) Model

- Simple Security: Subject S can read object O only if:
    - Label S dominates label O
    - Information can flow from label O to label S
    - No read up
- \* property: Subject can write object O only if:
    - Label O dominates label S
    - Information can flow from label S to label O
    - No write down

![Bell LaPadula Model](/img/cyber-security/y1/blp-model.png)

### Role Based Access Control

**RBAC** is a newer method of access control than **MAC** and **DAC**.

Sets of controls are centrally administered.

Permissions are assigned based upon roles, for example, a University would have different access for students and lecturers.

RBAC is useful for companies with high employee turnovers.

#### Roles vs Groups

- **Groups** are a set of users, and **roles** are a set of users as well as permissions
- **Roles** can be activated and deactivated, wheresa **groups** cannot
- Permissions for a **role** can be enumerated

#### RBAC Relations

- **User-role assignment**:
    - A user can be a member of many roles
    - Each role can have many users as members
- **Permission-role assignment**:
    - A permission can be assigned to many roles
    - Each role can have many permissions

![RBAC](/img/cyber-security/y1/rbac.png)
