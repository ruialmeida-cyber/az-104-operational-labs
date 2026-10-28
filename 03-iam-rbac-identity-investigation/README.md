# Lab 03 — IAM and RBAC Identity Investigation

## Overview

This lab explores identity management and access control in Microsoft Azure using the Azure Portal, Azure CLI, and Microsoft Graph.

The objective was to investigate user identities, review Role-Based Access Control (RBAC), query directory information, and check whether devices were registered in the Microsoft Entra ID tenant.

## Objectives

* Explore Azure identity and access management.
* Review RBAC assignments at resource-group scope.
* Understand security groups and role assignments.
* Use Azure CLI to inspect the active Azure context.
* Query Microsoft Graph for directory users and devices.
* Distinguish internal member accounts from external guest accounts.
* Investigate registered device information.
* Document findings and environment limitations.

## Environment and Tools

* Microsoft Azure Portal
* Azure CLI
* Microsoft Graph API
* Microsoft Entra ID
* Azure Role-Based Access Control (RBAC)

Tenant-specific identifiers and personal identity details are excluded from this public portfolio.

## 1. Azure Portal — RBAC Investigation

The first part of the lab focused on identity and permissions through the Azure Portal.

A security group was used to explore group-based access management. The Reader role was examined at resource-group scope to understand how permissions can be assigned without granting unnecessary administrative privileges.

### Key Concepts

**Security groups**

Security groups help organise users and manage access through group membership rather than assigning permissions individually to every user.

**Role-Based Access Control (RBAC)**

Azure RBAC determines what actions identities can perform on Azure resources and the scope at which those permissions apply.

**Reader role**

The Reader role allows users to view Azure resources without granting permission to modify or delete them.

**Scope**

The scope of a role assignment determines which resources the permissions cover. A resource-group-level assignment applies to the relevant resources within that group, subject to Azure RBAC inheritance and other applicable permissions.

### Outcome

This investigation reinforced the importance of assigning permissions at the appropriate scope and following the principle of least privilege.

## 2. Azure CLI — Validate the Active Context

Azure CLI was used to inspect the currently authenticated Azure context.

Command:

```bash
az account show
```

This command displays information about the active Azure account and subscription context.

It helps confirm which Azure environment is selected before running additional commands.

### Investigation Points

* Confirm the active Azure account context.
* Identify the selected subscription.
* Validate the context before administrative operations.
* Avoid running commands against an unintended subscription.

**Security note:** Review command output before publishing it. Subscription IDs and other tenant-specific information should not be exposed unnecessarily.

## 3. Microsoft Graph — Investigate Directory Users

Microsoft Graph was queried to retrieve directory user objects.

Command:

```bash
az rest --method GET --url "https://graph.microsoft.com/v1.0/users"
```

The results depend on the authenticated identity and the permissions available to it.

### Member Accounts

Member accounts generally represent identities associated with an organisation's own directory.

### Guest Accounts

Guest accounts commonly represent external users invited to collaborate within an organisation.

An external guest account may contain `#EXT#` in its user principal name. This is a common indicator of a Microsoft Entra B2B guest identity, although the account's directory properties should be used to confirm its identity type.

### Investigation Findings

The directory investigation identified an internal member identity and an external guest identity.

This demonstrated that a Microsoft Entra ID directory can contain different identity types with different organisational relationships.

The existence of a directory user does not automatically mean that the user has access to a particular Azure resource. Effective access also depends on role assignments, group memberships, scope, and other applicable access controls.

**Security note:** Personal email addresses, user principal names, object IDs, and other identifying directory properties have been excluded from this public report.

## 4. Microsoft Graph — Investigate Registered Devices

Microsoft Graph was also queried to investigate directory device objects.

Command:

```bash
az rest --method GET --url "https://graph.microsoft.com/v1.0/devices"
```

This request retrieves device objects visible to the authenticated identity, subject to the available permissions.

### Finding

The query returned an empty `value` collection:

```json
{
  "value": []
}
```

This indicated that no device objects were returned in the accessible result set at the time of the investigation.

It does not prove that no physical computers existed in the environment. The result reflects the query, permissions, and tenant context available during the investigation.

### Why Device Registration Matters

Device registration can support identity and access controls, including scenarios involving device-based access requirements.

Investigating device objects helps distinguish directory identity information from device registration status.

## 5. Windows 11 Device Registration — Environment Limitation

An attempt was made to explore Windows 11 device registration.

The required prerequisites were unavailable in the lab environment, so the registration workflow could not be completed.

This limitation was documented rather than presenting an unsuccessful or incomplete registration as a successful result.

### Lessons Learned

* Device registration depends on the available tenant configuration and device prerequisites.
* An empty device query and an unavailable registration workflow are separate findings.
* Environment limitations should be recorded clearly in technical documentation.
* Further validation would be required in a suitably configured environment.

## 6. Key Findings

| Area                | Finding                                                                                             |
| ------------------- | --------------------------------------------------------------------------------------------------- |
| Azure context       | The active account and subscription context can be inspected with Azure CLI.                        |
| RBAC                | Role assignments define permitted actions and their applicable scope.                               |
| Security groups     | Group-based access management helps organise identities and permissions.                            |
| Directory users     | Microsoft Graph can be used to investigate directory user objects.                                  |
| Identity types      | The investigation identified an internal member and an external guest identity.                     |
| Directory devices   | The device query returned an empty `value` collection.                                              |
| Device registration | Windows 11 registration could not be completed because the required prerequisites were unavailable. |
| Security hygiene    | Tenant-specific identifiers and personal identity details should be excluded from public evidence.  |

## 7. Security Considerations

This lab reinforced several important identity-security principles.

### Least Privilege

Permissions should be limited to the actions and resources required for a user's responsibilities.

### Scope Awareness

An RBAC assignment must be evaluated in the context of its scope and any applicable inherited permissions.

### Group-Based Access

Security groups provide a manageable way to organise identities and apply permissions consistently.

### Identity Classification

Internal members and external guests should be distinguished when reviewing directory users and access requirements.

### Evidence Protection

Public documentation should avoid exposing subscription IDs, tenant IDs, personal email addresses, object IDs, access tokens, or other sensitive environment details.

### Validation Before Action

The active Azure context should be checked before executing commands that could modify resources or permissions.

## 8. What I Learned

Through this lab, I developed a better understanding of how Azure identity and access management can be investigated through the portal and command-line tools.

The exercise demonstrated how to:

* Review RBAC concepts and resource-group scope.
* Inspect the active Azure CLI context.
* Query directory information through Microsoft Graph.
* Distinguish internal member identities from external guest identities.
* Investigate registered device objects.
* Record environment limitations accurately.
* Document security findings without exposing sensitive identifiers.

The lab also highlighted that identity, authorisation, and device registration are related but distinct areas of investigation. A directory user existing in Microsoft Entra ID does not automatically mean that the user has a particular Azure role or that a device is registered.

## 9. Conclusion

This lab provided practical experience investigating Azure identity and access management using the Azure Portal, Azure CLI, and Microsoft Graph.

The results demonstrated how directory users, RBAC permissions, and device objects can be examined as separate components of an identity-security investigation.

Although Windows 11 device registration could not be completed because the necessary prerequisites were unavailable, the limitation was documented and the available directory evidence was assessed.

These skills provide a foundation for further work involving Microsoft Entra ID, Azure RBAC, identity governance, and access-control validation.

## AZ-104 Relevance

This lab supports practical learning related to the Microsoft Azure Administrator certification, particularly:

* Managing Azure identities.
* Understanding role assignments and access scopes.
* Reviewing Azure RBAC permissions.
* Using Azure CLI for administration and validation.
* Investigating identity-related information using Microsoft Graph.
* Applying least-privilege principles.

---

**Lab status:** Completed with documented environment limitations.
