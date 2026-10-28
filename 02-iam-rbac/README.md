# Lab 02 — Azure Identity and Access Management (IAM) and Role-Based Access Control (RBAC)

## Overview

This lab demonstrates fundamental identity and access management concepts in Microsoft Azure using Microsoft Entra ID and Azure Role-Based Access Control (RBAC).

The lab focuses on security group management, group-based role assignment, and access control at the resource group scope.

## Objectives

* Create a security group in Microsoft Entra ID.
* Add a user to the security group.
* Verify group membership and identity structure.
* Assign the built-in Reader role to a security group at resource group scope.
* Understand the relationship between identity, role assignments, and Azure resource permissions.

## Environment

| Setting            | Value                |
| ------------------ | -------------------- |
| Cloud platform     | Microsoft Azure      |
| Identity provider  | Microsoft Entra ID   |
| Azure subscription | Azure subscription 1 |
| Region             | West Europe          |
| Resource group     | `rg-az104-labs`      |
| Security group     | `az104-rg-readers`   |
| Assigned role      | Reader               |
| Assignment scope   | Resource group       |

## Implementation

### 1. Create a Security Group

Created a security group in Microsoft Entra ID to centralise access management and avoid assigning permissions to individual users unnecessarily.

### 2. Add a User to the Group

Added the active Azure user account to the security group and verified the membership.

### 3. Verify the Identity Structure

Confirmed that the user was a member of the security group in Microsoft Entra ID.

### 4. Assign the Reader Role

Assigned the built-in **Reader** role to the `az104-rg-readers` security group at the `rg-az104-labs` resource group scope.

This allows eligible group members to view resources within the assigned scope without granting permission to modify them.

## Key Concepts

* **Microsoft Entra ID:** Manages identities, groups, and directory-related access.
* **Azure RBAC:** Controls access to Azure resources through role assignments.
* **Security groups:** Allow permissions to be managed centrally for multiple users.
* **Scope:** Defines where a role assignment applies, such as a subscription, resource group, or individual resource.
* **Least privilege:** The Reader role provides visibility without granting resource modification permissions.

## Evidence

The lab includes the following screenshots:

* `Members.png` — Evidence of group membership.
* `RBAC.png` — Evidence of the role-based access control configuration.
* `Readers_Group.png` — Evidence of the security group.
* `Resource Group.png` — Evidence of the resource group.

## Outcome

The security group was assigned the Reader role at resource group scope. The configuration demonstrates how Azure permissions can be managed through group-based role assignments.

## Security Considerations

* Use group-based assignments where appropriate to simplify access management.
* Apply permissions at the narrowest practical scope.
* Avoid assigning broad administrative privileges when read-only access is sufficient.
* Review group membership and role assignments periodically.

## AZ-104 Relevance

This lab supports preparation for the Microsoft Azure Administrator (AZ-104) certification, particularly identity management, Azure RBAC, security groups, and resource-level access control.
