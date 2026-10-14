# PearlMart Boundary-Flow Checklist

This checklist compares the corrected diagrams and flow specification. **Status is based on the files in this package**, not on a live GitHub review.

## Level 0 → Level 1

| Level 0 boundary | Level 1 realization | Status |
|---|---|---|
| Administrator → System: login/password data; inventory update | Login/password to 1.0; update data to 2.0 | PASS |
| System → Administrator: authentication; update confirmation | 1.0 → Administrator; 2.0 → Administrator | PASS |
| Inventory Manager → System: login/password; inventory/order/report requests | 1.0, 2.0, 3.0 and 6.0 | PASS |
| System → Inventory Manager: authentication; inventory/expiry; order/request summary; reports | 1.0, 2.0, 3.0 and 6.0 → Inventory Manager | PASS |
| Store Manager → System: login/password; received-goods verification | 1.0 and 3.0 | PASS |
| System → Store Manager: authentication; delivery/receiving information and confirmation | 1.0 and 3.0 → Store Manager | PASS |
| Salesperson → System: login/password; sales and completion/cancel decision; replacement/customer requests | 1.0, 4.0 and 5.0 | PASS |
| System → Salesperson: authentication; availability/amount/receipt; replacement result | 1.0, 4.0 and 5.0 | PASS |
| Supplier → System: response, invoice and delivery information | Supplier → 3.0 | PASS |
| System → Supplier: purchase-order details | 3.0 → Supplier | PASS |

## Process 4.0 → Level 2

| Process 4.0 boundary flow | Level 2 realization | Status |
|---|---|---|
| Salesperson → 4.0: sales transaction data / completion decision | Salesperson → 4.1 for transaction data; Salesperson → 4.4 for decision | PASS |
| D2 → 4.0: item, price and available quantity | D2 → 4.2 | PASS |
| 4.0 → Salesperson: item availability result | 4.2 → Salesperson | PASS |
| Salesperson → 4.0: complete/cancel decision | Salesperson → 4.4 | PASS |
| 4.0 → Salesperson: sale amount/receipt/transaction result | 4.5 → Salesperson | PASS |
| 4.0 → D2: sold quantity updates | 4.5 → D2 | PASS |
| 4.0 → D5: transaction records | 4.4 → D5 for cancellation; 4.5 → D5 for completed sale | PASS |

## Structural and business-rule checks

- [x] Level 0 contains one process and no data stores.
- [x] Level 1 contains processes 1.0–6.0 and data stores D1–D6.
- [x] Level 2 decomposes Process 4.0 using subprocesses 4.1–4.5.
- [x] Customer requests reach Process 3.0 for supplier-order review.
- [x] Replacement transactions are written to D5.
- [x] Availability is returned from 4.2; cancellation does not deduct stock.
- [x] Completed sales are recorded in D5 and update sold quantity in D2.

**Overall DFD balancing: PASS.** This does not certify the missing group-level Milestone 1 report or a live GitHub merge.
