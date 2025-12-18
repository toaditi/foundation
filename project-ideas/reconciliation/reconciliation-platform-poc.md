# Reconciliation Platform - POC

## 1. POC Objective

The objective of this POC is to validate the reconciliation approach using a narrowly scoped, high-value use case.

This POC will prove that:

- Data can be safely collected from multiple systems
- Reconciliation logic can be executed independently
- Results are clear and actionable

## 2. POC Scope

### In Scope

- Order creation reconciliation
- POS <-> OMS only
- Presence validation of orders

### Out of Scope

- Fulfillment, returns, payments
- Real-time reconciliation
- Automated remediation
- Advanced reporting or alerting

## 3. Core Reconciliation Question

> Does `POS.order_id` exist in OMS?

This single question defines the POC logic and success criteria.

## 4. Systems Involved

- POS - Source of order creation
- OMS - Downstream system expected to receive orders
- Reconciliation Service - Standalone validation layer

## 5. Data Collection Approach (POC)

### Preferred Method: File-Based Ingestion

- CSV files generated from POS and OMS
- Files dropped to a known SFTP location
- Each reconciliation run processes:

  - One POS file
  - One OMS file

### Future-Compatible Alternatives

- REST APIs
- GraphQL queries

## 6. Standalone Architecture (POC)

- The reconciliation service will:

  - Run independently
  - Use its own database
  - Avoid querying or manipulating the commerce DB directly

This ensures:

- No production performance risk
- Safe handling of large datasets

## 7. Reconciliation Logic (POC)

1. Ingest POS order data
2. Ingest OMS order data
3. Store both datasets in reconciliation DB
4. Compare using:

   - `order_id` as the primary key

5. Identify:

   - Orders present in POS but missing in OMS

## 8. Output and Results

The POC will produce:

- A queryable dataset or view
- Clear indicators for:

  - Matched orders
  - Missing OMS orders

The output should be simple, inspectable, and easy to validate.

## 9. Operational Flow

1. Data is received (CSV)
2. Data is persisted
3. Reconciliation logic runs
4. Results are stored and exposed

## 10. POC Success Criteria

The POC is successful if:

- POS and OMS data can be reconciled independently
- Missing orders are reliably identified
- No impact occurs on core commerce systems
- The approach is clearly extensible to future use cases
