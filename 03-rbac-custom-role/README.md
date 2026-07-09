# Lab 3 – Custom Azure RBAC Role

## Objective

Create a custom Azure RBAC role scoped to the `rg-az104-labs` resource group.

The role provides limited permissions for Azure virtual machine operations without granting unnecessary administrative privileges.

This lab demonstrates Azure Role-Based Access Control (RBAC) fundamentals, including:

- Creating a custom RBAC role
- Selecting specific permissions
- Applying least privilege principles
- Restricting role scope
- Validating the role using Azure CLI

---

## Environment

| Resource | Value |
|---|---|
| Resource Group | `rg-az104-labs` |
| Role Type | Custom Azure RBAC Role |
| Scope | Resource Group |

---

# Custom Role

## Role Name

`Lab VM Operator`

## Description

Custom role for AZ-104 lab with limited virtual machine permissions.

---

# Permissions Granted

The custom role contains the following Azure RBAC actions:

## Virtual Machine Read Access

```text
Microsoft.Compute/virtualMachines/read
```

Allows viewing virtual machine properties.

---

## Start Virtual Machine

```text
Microsoft.Compute/virtualMachines/start/action
```

Allows starting Azure virtual machines.

---

## Resource Group Read Access

```text
Microsoft.Resources/subscriptions/resourceGroups/read
```

Allows reading resource group information.

---

# Assignable Scope

The custom role was restricted to:

```text
/subscriptions/<subscription-id>/resourceGroups/rg-az104-labs
```

Scope:

```text
Resource Group
```

The role is limited to the resource group level instead of the entire subscription.

---

# Least Privilege Design

This role was designed following the principle of least privilege.

## Allowed Actions

- Read virtual machine properties
- Start virtual machines
- Read resource group information

## Actions Not Granted

The role does not allow:

- Creating resources
- Deleting resources
- Modifying virtual machines
- Restarting virtual machines
- Stopping virtual machines
- Assigning Azure roles
- Managing permissions

---

# JSON Permission Definition

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

---

# Azure CLI Validation

The custom role was validated using Azure CLI:

```bash
az role definition list --name "Lab VM Operator" --output table
```

Output:

```text
Name             Type                                     Description
---------------  ---------------------------------------  --------------------------------------------------------------------
Lab VM Operator  Microsoft.Authorization/roleDefinitions  Custom role for AZ-104 lab with limited virtual machine permissions.
```

---

# Evidence Collected

- Custom role permissions configured in Azure Portal
- Resource group assignable scope configured
- JSON role definition reviewed
- Azure CLI validation completed

---

# Skills Demonstrated

- Azure RBAC custom role creation
- Permission-level access control
- Least privilege implementation
- Resource group scope limitation
- Azure CLI validation

---

# Lab Outcome

Successfully created and validated a custom Azure RBAC role:

```text
Lab VM Operator
```

The role was scoped to:

```text
rg-az104-labs
```

and verified using Azure CLI.
