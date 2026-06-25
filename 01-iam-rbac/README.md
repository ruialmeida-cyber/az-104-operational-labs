# IAM and RBAC Lab (Azure Portal)

## Objective

The purpose of this lab is to understand and implement Microsoft Entra ID identity management and Role-Based Access Control (RBAC) in Azure using the Azure Portal.

---

## Environment

- Azure Subscription: Azure subscription 1
- Directory: Default Entra ID tenant
- Role: Subscription Owner (lab environment)
- Region: West Europe

---

## Lab Steps

### 1. Created a security group in Entra ID
A security group was created to manage access centrally instead of assigning roles directly to users.

### 2. Added user to the group
The active Azure user account was added as a member of the security group.

### 3. Verified identity structure
Confirmed user membership inside Entra ID and validated group membership.

### 4. Assigned RBAC role at Resource Group level
The following configuration was applied:

- Scope: Resource Group (rg-az104-labs)
- Role: Reader
- Assignment target: Security group (az104-rg-readers)

---

## Key Concepts Learned

- Difference between Entra ID (identity) and Azure RBAC (permissions)
- Role-based access control is applied at scope (subscription / resource group / resource)
- Group-based assignment is best practice over direct user assignment
- Permissions are inherited through group membership

---

## Outcome

The security group successfully received Reader access to the target Resource Group. The user inherited permissions through group membership.

---

## Notes

This lab is part of AZ-104 operational practice and focuses on identity and access management fundamentals in Azure.
