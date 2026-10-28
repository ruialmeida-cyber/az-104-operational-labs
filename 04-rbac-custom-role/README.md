# Lab 04 — Custom Azure RBAC Role

## Overview

This lab demonstrates how to create and validate a custom Azure Role-Based Access Control (RBAC) role using the Azure Portal and Azure CLI.

The role, named `Lab VM Operator`, was designed to provide limited permissions for viewing and starting Azure virtual machines within a specific resource group.

The objective is to apply the principle of least privilege by granting only the permissions required for the intended operational tasks.

## Objectives

* Create a custom Azure RBAC role.
* Define explicit permissions using Azure RBAC actions.
* Restrict the role's assignable scope to a resource group.
* Distinguish permitted actions from administrative privileges.
* Validate the custom role definition using Azure CLI.
* Document the configuration and supporting evidence.

## Environment

| Component           | Configuration              |
| ------------------- | -------------------------- |
| Cloud platform      | Microsoft Azure            |
| Access control      | Azure RBAC                 |
| Resource group      | `rg-az104-labs`            |
| Role type           | Custom role                |
| Custom role name    | `Lab VM Operator`          |
| Assignable scope    | Resource group             |
| Configuration tools | Azure Portal and Azure CLI |

---

## 1. Custom Role Definition

### Role Name

`Lab VM Operator`

### Description

Custom role for AZ-104 lab with limited virtual machine permissions.

### Design Principle

The role follows the principle of least privilege by limiting the available operations to virtual machine read access, virtual machine start, and resource group read access.

Creating a role definition does not automatically grant a user these permissions. The role must also be assigned to an identity at an applicable scope before that identity receives the role's permissions.

---

## 2. Permissions Granted

The custom role includes the following Azure RBAC actions.

### Read Virtual Machine Properties

```text
Microsoft.Compute/virtualMachines/read
```

Allows the assigned identity to read virtual machine properties.

### Start Virtual Machines

```text
Microsoft.Compute/virtualMachines/start/action
```

Allows the assigned identity to start virtual machines within the applicable scope.

### Read Resource Group Information

```text
Microsoft.Resources/subscriptions/resourceGroups/read
```

Allows the assigned identity to read resource group information.

---

## 3. Assignable Scope

The custom role was restricted to the following resource group scope:

```text
/subscriptions/<subscription-id>/resourceGroups/rg-az104-labs
```

Replace `<subscription-id>` with the appropriate subscription identifier when using the scope in an actual configuration.

### Scope Design

The role's assignable scope is limited to the `rg-az104-labs` resource group rather than the entire subscription.

This reduces the role's intended scope of use and supports more granular access management.

**Important distinction:** The role definition's `assignableScopes` property determines where the role can be assigned. The scope used when creating a role assignment determines the resources to which that assignment applies. Both should be configured appropriately.

---

## 4. Least Privilege Analysis

### Allowed Actions

The role permits the following operations:

* Read virtual machine properties.
* Start virtual machines.
* Read resource group information.

### Actions Not Explicitly Granted

The custom role does not explicitly grant permissions to:

* Create virtual machines.
* Delete virtual machines.
* Modify virtual machine configuration.
* Restart virtual machines.
* Stop or deallocate virtual machines.
* Create or modify Azure role assignments.
* Manage access permissions.

The effective permissions of an identity can also be influenced by other role assignments, inherited permissions, and applicable Azure authorisation rules. The custom role alone should not be treated as proof that an identity has no other permissions.

---

## 5. JSON Permission Definition

The following JSON illustrates the role's permission actions.

```json
{
  "actions": [
    "Microsoft.Compute/virtualMachines/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Resources/subscriptions/resourceGroups/read"
  ],
  "notActions": [],
  "dataActions": [],
  "notDataActions": []
}
```

This is the permissions section of a custom role definition, not a complete role definition file. A complete custom role definition also includes properties such as `Name`, `IsCustom`, `Description`, and `AssignableScopes`.

---

## 6. Azure CLI Validation

The custom role was validated using Azure CLI.

### Command

```bash
az role definition list --name "Lab VM Operator" --output table
```

### Validation Objective

The command retrieves role definitions matching the specified name and displays the results in table format.

The validation checks that the custom role definition exists and that Azure recognises it as a role definition.

For a more detailed inspection of the permissions and assignable scopes, use:

```bash
az role definition list --name "Lab VM Operator" --output json
```

### Observed Result

The lab output showed the `Lab VM Operator` role definition with the type:

```text
Microsoft.Authorization/roleDefinitions
```

This confirmed that the role definition could be retrieved using Azure CLI.

---

## 7. Evidence Collected

The lab includes the following screenshots:

| File                             | Evidence                          |
| -------------------------------- | --------------------------------- |
| `01-custom-role-basics.png`      | Initial custom role configuration |
| `02-custom-role-permissions.png` | Configured role permissions       |
| `03-custom-role-scope.png`       | Assignable scope configuration    |
| `04-custom-role-created.png`     | Created custom role               |

These screenshots support the documented configuration and provide visual evidence of the role creation process.

---

## 8. Skills Demonstrated

* Azure RBAC custom role creation.
* Permission-level access control.
* Least privilege design.
* Resource group scope configuration.
* Azure role definition structure.
* Azure CLI role validation.
* Technical evidence collection and documentation.

---

## 9. Key Learning Points

* Azure RBAC custom roles allow permissions to be tailored to operational requirements.
* Azure RBAC actions define the management operations permitted by a role.
* Assignable scopes constrain where a custom role can be used.
* Creating a role definition is different from assigning that role to a user, group, or service principal.
* Azure CLI provides a practical way to inspect and validate role definitions.
* Least privilege requires reviewing both the role's permissions and the identity's other effective access.

---

## 10. Conclusion

This lab demonstrated the creation and validation of a custom Azure RBAC role named `Lab VM Operator`.

The role was designed to permit virtual machine read access, virtual machine start operations, and resource group read access. Its assignable scope was restricted to the `rg-az104-labs` resource group.

The exercise reinforced the importance of explicit permissions, appropriate scope restrictions, least privilege, and command-line validation in Azure access control.

## AZ-104 Relevance

This lab supports preparation for the Microsoft Azure Administrator (AZ-104) certification, particularly Azure RBAC, custom role definitions, access scope, and Azure CLI administration.
