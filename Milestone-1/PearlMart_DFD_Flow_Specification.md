# PearlMart DFD Flow Specification

## DFD Level 0

**Process:** 0 - PearlMart Inventory Management System

### External entities and boundary flows

| External entity | To system | From system |
|---|---|---|
| Administrator | Login Credentials; Password Change Data; Administrative Update Data | Authentication Result; Update Confirmation |
| Inventory Manager | Login Credentials; Inventory Requests; Supplier Order Request; Report Request | Inventory Information; Order Status; Customer Request Information; Reports |
| Store Manager | Login Credentials; Received Goods Verification | Order / Delivery Information; Receiving Confirmation |
| Salesperson | Login Credentials; Item Barcode / ID; Purchase Quantity; Cancel Request; Replacement Request; Customer Item Request | Item Details; Availability; Sale Amount; Receipt; Transaction Result |
| Supplier | Order Response; Invoice Information; Delivery Information | Purchase Order Details |

## DFD Level 1

### Processes
1. **1.0 Authenticate & Manage User Access**
2. **2.0 Manage Inventory**
3. **3.0 Manage Supplier Orders & Receiving**
4. **4.0 Process Sales Transactions**
5. **5.0 Handle Replacements & Customer Requests**
6. **6.0 Generate Management Reports**

### Data stores
- **D1** User Accounts
- **D2** Inventory Records
- **D3** Inventory Activity Records
- **D4** Supplier Order Records
- **D5** Sales Transaction Records
- **D6** Customer Request Records

## DFD Level 2 - Process 4.0

### Subprocesses
1. **4.1 Capture Sale Item**
2. **4.2 Retrieve Item & Validate Quantity**
3. **4.3 Calculate Sale Amount**
4. **4.4 Complete or Cancel Transaction**
5. **4.5 Generate Receipt & Update Inventory**

### Detailed flows
- Salesperson -> 4.1: **Sales Transaction Data**
- 4.1 -> 4.2: **Item ID / Barcode / Quantity**
- D2 -> 4.2: **Item / Price / Available Quantity**
- 4.2 -> Salesperson: **Item / Availability Result**
- 4.2 -> 4.3: **Validated Item Details**
- 4.3 -> 4.4: **Calculated Amount**
- Salesperson -> 4.4: **Complete / Cancel Decision**
- 4.4 -> D5: **Cancelled Transaction Data**
- 4.4 -> 4.5: **Completed Transaction Data**
- 4.5 -> D5: **Completed Sales Transaction Data**
- 4.5 -> D2: **Sold Quantity Updates**
- 4.5 -> Salesperson: **Receipt / Transaction Result**

**Validation note:** when requested quantity exceeds available quantity, Process 4.2 returns an insufficient-quantity/availability result instead of proceeding to completion.
