# PearlMart Boundary-Flow Checklist

This checklist confirms balancing between DFD levels and supports GitHub Issue #13.

## Level 0 -> Level 1 balancing

| Boundary | Level 0 flow | Level 1 realization | Status |
|---|---|---|---|
| Administrator -> System | Login Credentials; Password Change Data; Administrative Update Data | Administrator -> 1.0 Authenticate & Manage User Access | PASS |
| System -> Administrator | Authentication Result; Update Confirmation | 1.0 -> Administrator | PASS |
| Inventory Manager -> System | Login Credentials; Inventory Requests; Supplier Order Request; Report Request | 1.0 / 2.0 / 3.0 / 6.0 receive the same logical inputs | PASS |
| System -> Inventory Manager | Inventory Information; Order Status; Customer Request Information; Reports | 2.0 / 3.0 / 5.0 / 6.0 produce the same logical outputs | PASS |
| Store Manager -> System | Login Credentials; Received Goods Verification | 1.0 and 3.0 | PASS |
| System -> Store Manager | Order / Delivery Information; Receiving Confirmation | 3.0 -> Store Manager | PASS |
| Salesperson -> System | Login Credentials; sale/cancel/replacement/customer-request inputs | 1.0 / 4.0 / 5.0 | PASS |
| System -> Salesperson | Item Details; Availability; Sale Amount; Receipt; Transaction Result | 4.0 and 5.0 | PASS |
| System -> Supplier | Purchase Order Details | 3.0 -> Supplier | PASS |
| Supplier -> System | Order Response; Invoice Information; Delivery Information | Supplier -> 3.0 | PASS |

## Level 1 Process 4.0 -> Level 2 balancing

| Process 4.0 boundary flow | Level 2 realization | Status |
|---|---|---|
| Salesperson -> 4.0: Sales Transaction Data | Salesperson -> 4.1 | PASS |
| Salesperson -> 4.0: Complete / Cancel Decision | Salesperson -> 4.4 | PASS |
| D2 -> 4.0: Item / Price / Quantity Data | D2 -> 4.2 | PASS |
| 4.0 -> Salesperson: Item / Availability Result | 4.2 -> Salesperson | PASS |
| 4.0 -> Salesperson: Receipt / Transaction Result | 4.5 -> Salesperson | PASS |
| 4.0 -> D2: Sold Quantity Updates | 4.5 -> D2 | PASS |
| 4.0 -> D5: Completed / Cancelled Transaction Data | 4.4 / 4.5 -> D5 | PASS |

## Consistency checks

- [x] Process numbering is consistent: 1.0-6.0 at Level 1 and 4.1-4.5 at Level 2.
- [x] Level 0 has no data stores.
- [x] Level 1 uses logical data stores D1-D6.
- [x] Level 2 does not introduce a new external entity.
- [x] Level 2 does not introduce a new boundary flow that is absent from Process 4.0.
- [x] Cancelled transactions are recorded without inventory deduction.
- [x] Completed transactions record the sale and update sold quantity.

**Overall balancing result: PASS**
