# 02 – IAM and RBAC Identity Investigation (Azure Portal + Azure CLI)

## Overview

This operational lab extends the previous RBAC configuration exercise by validating Microsoft Entra ID identities through Azure CLI and Microsoft Graph. The objective is to combine Azure Portal administration with API-based verification, following a SOC-style investigative workflow.

Unlike the previous lab, this exercise focuses on validating the current identity state of the tenant rather than simply configuring Azure resources.

---

# Objectives

- Configure RBAC using the Azure Portal.
- Validate Azure authentication using Azure CLI.
- Enumerate Microsoft Entra ID users using Microsoft Graph.
- Identify member and guest identities.
- Verify the current device inventory.
- Compare portal configuration with CLI evidence.

---

# Environment

| Component | Value |
|-----------|-------|
| Azure Subscription | Azure subscription 1 |
| Tenant | Default Directory |
| Region | West Europe |
| Local Environment | Windows 11 + WSL2 Ubuntu |
| Azure CLI | 2.87.0 |
| API | Microsoft Graph |

---

# Part 1 – Azure Portal (RBAC)

## Step 1 – Created a Security Group

Created a Microsoft Entra ID security group to centralise permission assignment.

---

## Step 2 – Added User to the Group

Added the lab user to the security group.

---

## Step 3 – Assigned RBAC Permissions

Configuration:

- Scope: Resource Group
- Role: Reader
- Assignment Target: Security Group

---

## Result

The RBAC assignment was successfully inherited through group membership.

---

# Part 2 – Azure CLI Investigation

## Verify Azure Authentication

Command

```bash
az account show
```

Output

```json
{
  "environmentName": "AzureCloud",
  "homeTenantId": "2c0009ed-1f8d-41a1-9d6c-836d6fc700ab",
  "id": "a8ce2a35-1b4d-4e71-866d-d455304fb671",
  "isDefault": true,
  "managedByTenants": [],
  "name": "Azure subscription 1",
  "state": "Enabled",
  "tenantDefaultDomain": "ruialmeidadacunhagmail.onmicrosoft.com",
  "tenantDisplayName": "Default Directory",
  "tenantId": "2c0009ed-1f8d-41a1-9d6c-836d6fc700ab",
  "user": {
    "name": "rui.almeidadacunha@gmail.com",
    "type": "user"
  }
}
```

### Observation

Azure CLI authentication was successful and confirmed the active subscription and tenant context.

---

# Enumerate Entra ID Users

Command

```bash
az rest --method GET --url "https://graph.microsoft.com/v1.0/users"
```

Output

```json
{
  "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users",
  "value": [
    {
      "displayName": "IAM Lab User 01",
      "id": "7cc3ad3f-e473-425e-8b79-f8c47d6c3ead",
      "userPrincipalName": "iam-lab-user-01@ruialmeidadacunhagmail.onmicrosoft.com"
    },
    {
      "displayName": "Rui Almeida Da Cunha",
      "id": "e725c212-4d94-4ae4-9bf1-62422d7bac76",
      "userPrincipalName": "rui.almeidadacunha_gmail.com#EXT#@ruialmeidadacunhagmail.onmicrosoft.com"
    }
  ]
}
```

### Observation

Microsoft Graph successfully enumerated all identities within the tenant.

Two identity types were identified:

- Internal member account
- External guest (B2B) account using the **#EXT#** naming convention

---

# Verify Device Inventory

Command

```bash
az rest --method GET --url "https://graph.microsoft.com/v1.0/devices"
```

Output

```json
{
  "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#devices",
  "value": []
}
```

### Observation

No device objects are currently registered within the Microsoft Entra ID tenant.

---

# Identity Analysis

This investigation confirmed:

- Azure CLI authentication is operational.
- Microsoft Graph API is accessible through Azure CLI.
- User identities can be enumerated without using the Azure Portal.
- The tenant currently contains both internal and guest identities.
- No registered Entra ID devices currently exist.

---

# Device Registration Investigation

An attempt was made to register a Windows 11 device with Microsoft Entra ID.

Although the identity layer was fully operational, device registration could not be completed because the required device enrolment prerequisites were not available within the current lab environment.

Rather than forcing an unsupported configuration, the investigation focused on validating the identity plane through Azure CLI and Microsoft Graph.

This reflects an important architectural distinction:

- Microsoft Entra ID manages identities.
- Azure RBAC manages permissions.
- Device registration depends on additional device trust and management prerequisites.

---

# Skills Demonstrated

- Microsoft Entra ID administration
- Azure RBAC
- Azure CLI
- Microsoft Graph
- Identity enumeration
- Tenant investigation
- Guest identity analysis
- API-based verification
- Evidence collection

---

# Key Learning Points

- Microsoft Entra ID identity management can be validated using Azure CLI and Microsoft Graph.
- Azure RBAC permissions should be assigned through groups rather than directly to users.
- Microsoft Graph provides direct visibility into tenant identities.
- Identity management, RBAC and device trust represent separate layers within Azure's security architecture.
- Operational validation through CLI complements Azure Portal administration.

---

# Conclusion

This lab combines Azure Portal administration with Azure CLI and Microsoft Graph investigation to validate identity and access management within Microsoft Entra ID.

The exercise demonstrates how GUI-based administration can be complemented by API-driven verification, providing a workflow that aligns more closely with operational cloud administration and SOC-style identity investigation.
