# Expense Reconciliation MVP

Mobile-first Streamlit prototype for ICICI bank + ICICI credit-card reconciliation.

## Design invariants
- Deterministic IDs: re-uploading the same statement must be idempotent.
- Bank ↔ CC settlements are relationships, not expenses.
- Refund-to-bank chains are relationships, not income.
- EMI conversion credits are contextual and must not be blindly classified as refunds.
- Multi-line CC rows are parsed as stateful records; parser failures are visible.
- Bank and CC dates are normalized to `YYYY-MM-DD` before reconciliation.
- Deloitte salary and reimbursement are separate concepts; classification rules must not sum all Deloitte credits into salary.
- Existing tracker convention `Settlement Log` is preserved as the role/expense export convention.
- `Involved` remains available for manual enrichment (Family, Friend Group, etc.).
- CSV export remains a permanent escape hatch; Google Sheets write-back is intentionally not part of MVP-1.

## Current prototype scope
1. Parse ICICI bank XLSX.
2. Parse ICICI CC PDFs with multi-line transaction support.
3. Classify settlement/refund/EMI roles.
4. Reconcile bank ↔ CC settlement pairs, including pending coverage.
5. Export expense candidates for manual review.
6. Provide a Streamlit UI.

## Important limitation
The current implementation is a prototype, not yet the production backfill engine. Before importing historical data into the real tracker, add full statement balance gates, tracker deduplication against existing rows, merchant/category rules, EMI contract tables, and Google Sheets persistence.
