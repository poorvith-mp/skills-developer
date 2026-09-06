---
name: salesforce
group: Domain-specific
description: >-
  Architect Salesforce: multi-cloud design, integration patterns, governor limits and deployment.
  Use when developing Apex, Lightning Web Components, or Salesforce flows.
---

# salesforce

## Core Philosophy
Salesforce enterprise development is not clicking around Setup menus or writing single-record Apex scripts. Salesforce is a multi-tenant cloud environment governed by strict, unyielding runtime **Governor Limits**. An un-bulkified SOQL query inside a `for` loop or an unhandled recursion trigger will instantly crash production workflows. Architecting Salesforce requires rigorous bulkification patterns, decoupled trigger frameworks, Lightning Web Components (LWC), and automated Salesforce DX metadata deployments.

---

## 4-Step Salesforce Enterprise Architecture

### Step 1: Governor Limits & Bulkification Discipline
1. **The Critical Limits (Synchronous Apex)**:
   - Total SOQL queries: **100** max.
   - Total DML statements: **150** max (max 10,000 records processed).
   - Total heap size: **6MB**.
   - Maximum CPU execution time: **10,000ms (10 seconds)**.
2. **The Golden Rule of Bulkification**:
   - Never write a SOQL query or DML operation (`insert`, `update`, `delete`) inside a `for` loop.
   - Always process records in batch collections (`List<Account>`, `Set<Id>`, `Map<Id, Account>`).

### Step 2: Trigger Architecture & Separation of Concerns
1. **The One-Trigger-Per-Object Rule**:
   - Never create multiple triggers on the same object (execution order is non-deterministic).
2. **The Handler Framework Pattern**:
   - Triggers must contain zero business logic. Triggers only dispatch to a structured Handler class:
     ```apex
     trigger AccountTrigger on Account (before insert, after update) {
         AccountTriggerHandler.handle(Trigger.new, Trigger.oldMap, Trigger.operationType);
     }
     ```
   - Implement recursion guards using static sets of IDs to prevent infinite trigger loops.

### Step 3: Modern Frontend with Lightning Web Components (LWC)
1. **LWC Architecture**:
   - Built on standard web components (Shadow DOM, Custom Elements, ECMAScript modern modules).
   - Use the Lightning Data Service (LDS) wire adapters (`@wire(getRecord)`) to read and mutate Salesforce data with client-side caching and zero custom Apex whenever possible.
2. **Asynchronous Apex for Heavy Workloads**:
   - Offload long-running computations to Queueable Apex or Batch Apex (`Database.Batchable`) to expand governor limits (SOQL increases to 200, CPU to 60s).

### Step 4: Salesforce DX & Metadata CI/CD
1. **Source-Driven Development**:
   - Store all metadata in version control (Git) in Salesforce DX source format (`force-app/main/default`).
   - Use scratch orgs for ephemeral feature development and testing:
     ```bash
     sf org create scratch -f config/project-scratch-def.json -a FeatureDevOrg
     sf project deploy start
     sf apex run test --code-coverage --result-format human
     ```
2. **Test Coverage Standards**:
   - Salesforce mandates 75% test coverage for production deployment; enforce **85%+** with meaningful asserts (test single record, bulk 200 records, and negative/permission failures).

---

## Deliverable Format: Salesforce Architecture Spec (`SFDC-SPEC.md`)

```markdown
# Salesforce Architecture Specification: [Feature / Module]

## 1. Data Model & Relationships
- **Objects Impacted**: `Account` (Standard), `Subscription__c` (Custom)
- **Relationship**: Master-Detail (`Subscription__c` -> `Account`)
- **Security**: Inherited sharing (`with sharing` enforced on all Apex classes)

## 2. Apex Trigger & Handler Design
```apex
public with sharing class SubscriptionTriggerHandler {
    public static void handleAfterInsert(List<Subscription__c> newRecords) {
        Set<Id> accountIds = new Set<Id>();
        for (Subscription__c sub : newRecords) {
            if (sub.AccountId__c != null) {
                accountIds.add(sub.AccountId__c);
            }
        }
        if (!accountIds.isEmpty()) {
            recalculateAccountARR(accountIds);
        }
    }
}
```

## 3. Governor Limit De-risking
- **Bulk Testing**: Test methods execute with 200 mock records to verify zero SOQL limit violations.
- **Asynchronous Processing**: Uses `Queueable` job for external HTTP callouts.

## 4. Deployment Checklist
- [ ] All Apex classes specify `with sharing` or `without sharing`.
- [ ] Test classes achieve >= 85% code coverage with `System.assertEquals()`.
- [ ] Scratch org deployment verifies zero metadata conflicts.
```

---

## Worked Example: Bulkified Opportunity ARR Rollup

- **Problem**: Legacy trigger fired individual SOQL queries per Opportunity line item, throwing `System.LimitException: Too many SOQL queries: 101` when importing bulk CSVs.
- **Refactor**: Replaced loop query with a single aggregated SOQL query grouped by Account ID stored in a `Map<Id, AggregateResult>`.
- **Result**: Successfully processed batches of 2,000 records in 1.2 seconds using only 3 SOQL queries.

---

## Verification Checklist

- [ ] Zero SOQL queries or DML statements reside inside `for` loops.
- [ ] Exactly one trigger per sObject, delegating to a structured Handler class.
- [ ] All Apex classes declare explicit sharing rules (`with sharing`).
- [ ] Apex test classes test bulk records ($\ge 200$ items) and verify assertions.
- [ ] Metadata deployed using Salesforce CLI (`sf project deploy start`) with clean git history.

---

## Anti-Patterns

- **SOQL in Loops**: Querying the database inside an iteration block, guaranteeing governor limit crashes in production.
- **Multiple Triggers per Object**: Creating 5 different triggers on `Contact`, leading to race conditions and debugging nightmares.
- **Hardcoding Record Type IDs**: Hardcoding 18-character Salesforce IDs instead of querying via DeveloperName or Schema describes.
