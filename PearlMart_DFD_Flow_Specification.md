# PearlMart DFD Flow Specification

## Scope and notation

This specification describes the Member 1 DFD contribution. It uses Gane–Sarson process/data-store notation and directional, named data flows. Level 0 contains one process and no stores.

## DFD Level 0 — Context

**Process 0:** PearlMart Inventory Management System

| External entity | To the system | From the system |
|---|---|---|
| Administrator | Login credentials; password-change data; inventory-update data | Authentication result; update confirmation |
| Inventory Manager | Login credentials; password-change data; inventory, supplier-order and report requests | Authentication; inventory and expired-goods information; order status and customer-request summary; reports |
| Store Manager | Login credentials; password-change data; received-goods verification | Authentication; delivery/receiving information; confirmation |
| Salesperson | Login credentials; password-change data; sales transaction data and completion/cancel decision; replacement/customer item-request data | Authentication; item availability; sale amount, receipt and transaction result; replacement/request result |
| Supplier | Order response; invoice; delivery information | Purchase-order details |

## DFD Level 1 — Processes and stores

| Process | Name |
|---|---|
| 1.0 | Authenticate & Manage User Access |
| 2.0 | Manage Inventory |
| 3.0 | Manage Supplier Orders & Receiving |
| 4.0 | Process Sales Transactions |
| 5.0 | Handle Replacements & Customer Requests |
| 6.0 | Generate Management Reports |

| Store | Name | Main contents |
|---|---|---|
| D1 | User Accounts | Role/account information and password updates |
| D2 | Inventory Records | Item, price, quantity and expiry data |
| D3 | Inventory Activity Records | Inventory changes and audit/activity records |
| D4 | Supplier Order Records | Purchase orders, supplier responses and receiving/order updates |
| D5 | Sales Transaction Records | Completed sales, cancellations and replacement transactions |
| D6 | Customer Request Records | Customer item requests for order review |

### Key internal flows

| From | To | Data flow |
|---|---|---|
| D1 | 1.0 | User account data |
| 1.0 | D1 | Password / account updates |
| D2 | 2.0 | Inventory records |
| 2.0 | D2 | Inventory record updates |
| 2.0 | D3 | Inventory activity records |
| 3.0 | D2 | Received quantity updates |
| 3.0 | D4 | Supplier order updates |
| D2 | 4.0 | Item / price / available quantity |
| 4.0 | D2 | Sold quantity updates |
| 4.0 | D5 | Completed / cancelled sales data |
| D5 | 5.0 | Original transaction data |
| 5.0 | D2 | Replacement inventory updates |
| 5.0 | D5 | Replacement transaction data |
| 5.0 | D6 | Customer item-request data |
| D6 | 3.0 | Customer requests for ordering |
| D2, D3, D4, D5 | 6.0 | Inventory/expiry, activity, supplier-order, and sales/replacement/cancellation data |

The complete external and store edge list is represented in the editable `.vpp` source. Same-direction related fields are grouped in composite flow labels at the context boundary.

### Level 1 → Level 2 balancing for Process 4.0

The Level 1 input **Sales Transaction Data / Completion Decision** is a composite parent flow. At Level 2 it is decomposed into **Sales transaction data** from the Salesperson to 4.1 and **Complete / cancel decision** from the Salesperson to 4.4. The Level 1 output **Availability / Sale Amount / Receipt / Transaction Result** is decomposed into the availability result from 4.2 and the sale amount, receipt and transaction result from 4.5.

## DFD Level 2 — Process 4.0

### Subprocesses

- **4.1 Capture Sale Item**
- **4.2 Retrieve Item & Validate Quantity**
- **4.3 Calculate Sale Amount**
- **4.4 Complete or Cancel Transaction**
- **4.5 Update Inventory & Finalize Sale**

### Detailed flows

| From | To | Data flow |
|---|---|---|
| Salesperson | 4.1 | Sales transaction data |
| 4.1 | 4.2 | Item ID / barcode / quantity |
| D2 | 4.2 | Item / price / available quantity |
| 4.2 | Salesperson | Item availability result |
| 4.2 | 4.3 | Validated item details |
| 4.3 | 4.4 | Calculated sale amount |
| Salesperson | 4.4 | Complete / cancel decision |
| 4.4 | D5 | Cancelled transaction data |
| 4.4 | 4.5 | Completed transaction data |
| 4.5 | D5 | Completed sales transaction data |
| 4.5 | D2 | Sold quantity updates |
| 4.5 | Salesperson | Sale amount / receipt / transaction result |

**Decision rule:** Process 4.2 returns an availability result if stock is insufficient and the sale does not proceed. A cancellation is recorded in D5 without changing D2. A completed sale is recorded in D5 and its sold quantity is deducted from D2.

## Assumptions

1. Authentication credentials and password changes are handled by Process 1.0; credentials are not sent to operational processes.
2. The Inventory Manager reviews customer item requests (D6) as part of supplier-order work (Process 3.0).
3. Store staff verify delivered goods before Process 3.0 commits received quantities to inventory.
4. Sales are recorded only after the salesperson confirms completion; cancellations remain auditable.
5. The Level 0 phrase “inventory information” includes expiry status so the boundary flow remains a composite of Level 1 outputs.

## Balancing summary

The boundary-flow checklist maps each external-entity input/output at Level 0 to matching Level 1 flows. Process 4.0’s input from the salesperson and D2, and outputs to the salesperson, D2 and D5, are represented at Level 2. See `Boundary_Flow_Checklist.md` for individual checks.
