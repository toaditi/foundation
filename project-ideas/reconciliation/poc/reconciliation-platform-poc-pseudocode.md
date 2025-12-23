# Reconciliation POC Pseudocode

Goal: Compare POS vs OMS order IDs from file-based extracts (CSV) and report missing IDs on each side.

Inputs (defaults):
- posFile = sftp://recon/inbox/pos_orders.csv
- omsFile = sftp://recon/inbox/oms_orders.csv
- posOrderIdField = order_id
- omsOrderIdField = order_id
- reconRunId = generated UUID
- logInputCounts = true

Pseudocode:
1) Create a reconciliation run record (reconRunId, source files, time window).
2) Resolve posFile and omsFile locations; download or stream if SFTP.
3) Read POS CSV (header=true).
4) Select posOrderIdField as order_id, trim, filter null/blank, drop duplicates.
5) Read OMS CSV (header=true).
6) Select omsOrderIdField as order_id, trim, filter null/blank, drop duplicates.
7) If logInputCounts: count each set and persist as run metrics.
8) onlyInPos = posDf left_anti join omsDf on order_id.
9) onlyInOms = omsDf left_anti join posDf on order_id.
10) Persist results:
    - onlyInPos => status MISSING_IN_OMS
    - onlyInOms => status MISSING_IN_POS
11) Store summary counts and mark the run complete.

Assumptions (POC):
- POS and OMS extracts cover the same time window.
- Order IDs are stable and comparable between systems.
- Reconciliation runs independently of POS/OMS databases.
- Output is stored in a reconciliation DB or a CSV report.

Supporting artifacts (POC):
- SFTP inbox/outbox for POS and OMS extracts
- Reconciliation database tables (runs, inputs, results)
- Job trigger (manual or scheduled)
