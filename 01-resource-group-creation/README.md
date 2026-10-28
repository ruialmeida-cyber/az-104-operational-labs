# Lab 0.1 — Azure Resource Group Creation

Microsoft Azure | Cloud Foundations | Resource Organisation

---

## Overview

This lab establishes the foundational Azure environment by creating and validating a Resource Group.

A Resource Group is a logical container used to organise and manage Azure resources such as virtual machines, networks, and storage services.

This provides the operational boundary for all subsequent labs in this portfolio.

---

## Objective

To establish a structured and controlled Azure environment by:

* Creating a Resource Group
* Defining subscription scope
* Selecting deployment region (West Europe)
* Validating an empty baseline environment

---

## Steps Performed

### 1. Azure Portal Access

* Logged into Microsoft Azure Portal
* Navigated to Resource Groups service

### 2. Resource Group Creation

* Initiated “Create Resource Group”
* Subscription: Azure subscription 1
* Resource Group Name: `rg-azure-labs-core-weu`
* Region: West Europe (EU West)

### 3. Validation

* Confirmed successful creation
* Verified Resource Group exists in Azure Portal
* Confirmed no resources deployed within the group

---

## Evidence

* Resource Group created and visible in Azure Portal
* Name: `rg-azure-labs-core-weu`
* Subscription: Azure subscription 1
* Region: West Europe
* Confirmed empty state (no deployed resources present)

---

## Outcome

A clean Azure Resource Group was successfully created and validated.

This establishes:

* A structured environment for future Azure deployments
* A controlled boundary for lab-based experimentation
* A consistent baseline for cloud administration practice

---

## Key Concepts Learned

* Azure Resource Groups as logical resource containers
* Subscription and region configuration in Azure
* Cloud environment structuring principles
* Importance of baseline environments before deployment

---

## Operational Significance

In enterprise Azure environments, Resource Groups are used to:

* Organise workloads by application or lifecycle
* Apply RBAC at scope level
* Support cost tracking and governance
* Enable controlled deployment and teardown of infrastructure

---

## Next Lab

**Lab 1.2 — Virtual Network Architecture (Planned)**

Expands this environment by introducing network segmentation and controlled resource communication.

---

## Repository Purpose

This lab forms part of a structured Azure learning progression covering:

* Cloud administration fundamentals
* Identity-aware infrastructure design
* Operational Azure environment management
