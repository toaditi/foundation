# Reconciliation Run Data Model

This document defines the **Reconciliation Run configuration data model**, designed using **UDM principles** and aligned with **Moqui framework entities**.

The model focuses on **configuration and definition storage** only.  
Execution, auditing, and result storage are intentionally out of scope.

---

## Entity Relationship Diagram

![Reconciliation Run Entity Diagram](./Reconciliation_ER_Diagram.png)

> **Note:**  
> - The diagram above is the authoritative visual representation.  
> - The source configuration is maintained separately from execution logic.

---

## Model Goals

- Define *what* should be reconciled, not *how*
- Enable reusable reconciliation runs across clients
- Leverage Moqui-native entities wherever possible
- Keep configuration declarative and schedulable

---

## Core Entities

### Reconciliation
A **schedulable parent entity** that groups one or more reconciliation runs.

**Purpose**
- Acts as the orchestration boundary
- Defines scheduling cadence
- Scoped to a client via `Party`

**Key Fields**
- `reconciliation_id`
- `reconciliation_name`
- `schedule_expr`
- `party_id`
- `is_active`

---

### ReconciliationRun
Defines a **single reconciliation check** within a reconciliation.

**Purpose**
- Represents one atomic comparison or validation
- Executed as part of a reconciliation group
- Reusable across clients if needed

**Key Fields**
- `reconciliation_run_id`
- `reconciliation_id`
- `run_name`
- `data_domain` (orders, returns, shipments)
- `purpose` (created_sync, status_match, financial_match)
- `default_time_window`
- `ruleset_id`
- `run_sequence`

---

### Party (Moqui)
Represents the **client / merchant / tenant**.

**Purpose**
- Multi-tenant isolation
- Ownership of reconciliation configurations

**Key Fields**
- `party_id`
- `party_type`
- `party_name`

---

### DataDocument (Moqui)
Defines a **canonical data point** used in reconciliation.

**Purpose**
- Reusable metric definitions
- Source-agnostic representation of data

**Examples**
- Order count
- Total order amount
- Shipment count by status

**Key Fields**
- `data_document_id`
- `data_document_name`
- `primary_entity_name`

---

### RunDataDocument
Associates **DataDocuments with a ReconciliationRun**.

**Purpose**
- Applies run-specific filters and aggregations
- Controls which metrics are mandatory

**Key Fields**
- `reconciliation_run_id`
- `data_document_id`
- `filter_expression`
- `aggregation`
- `is_required`

---

### SystemMessageRemote (Moqui)
Represents an **external or internal system instance**.

**Purpose**
- Defines where data is sourced from
- Encapsulates integration details

**Examples**
- Shopify (Prod)
- OFBiz (Stage)
- NetSuite (Prod)

**Key Fields**
- `system_message_remote_id`
- `remote_system_type`
- `remote_system_name`
- `environment`
- `partyId`

---

### RunSystemInstance
Associates systems with a reconciliation run.

**Purpose**
- Defines the role of each system in a run
- Supports source / target / peer comparisons

**Key Fields**
- `reconciliation_run_id`
- `system_message_remote_id`
- `role`

---

### RuleSet & Rule
Defines **conclusion logic** for reconciliation runs.

**Purpose**
- Determines success, warnings, or failures
- Encapsulates business tolerances and thresholds

**RuleSet Key Fields**
- `ruleset_id`
- `name`
- `version`

**Rule Key Fields**
- `rule_id`
- `rule_type`
- `expression`
- `severity`

---

## What Is Out of Scope (By Design)

- Execution tracking
- Data pull results
- Rule evaluation outcomes
- Alerts and notifications

These concerns will be introduced in a separate **execution-layer model**.

---

## Future Enhancements

- Execution entities (`ReconciliationExecution`, `RunExecution`)
- Rule evaluation result storage
- Alerting and notification hooks
- Moqui entity XML generation

