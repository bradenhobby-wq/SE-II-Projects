# Feature: Supplier Order Management
**Feature ID:** 4
**Branch pattern:** `feature/supplier_orders_management`
**Status:** First Draft
**Created:** 2026-10-06
**Input:** Maintain supplier orders - add, update, and deactivate orders. Also makes an order when stock gets low
**Depends on:** [Feature 10 — Merchandise Management](feature-10-merchandise-management.md) [Feature 11 - User Authentication And Verification](feature-11-user-authentication-and-verification.md)

## User Stories
### US-4.1: Add Orders
**As a** inventory/shipping clerk
**I want to** add Supplier Orders to be ordered on the specified date
**So that** we can restock our inventory

**Priority:** P1
**Independent test:** As an inventory/shipping clerk, send a Supplier Order to an office email and verify it sent correctly
**Acceptance scenarios:** see ### US-4.1 under Acceptance
Criteria

### US-4.2: Edit Orders
**As a** inventory/shipping clerk
**I want to** edit supplier orders
**So that** incorrect entries can be corrected

**Priority:** P1
**Independent test:** Send a supplier order, edit information, and check to see if the supplier is notified of the changes
**Acceptance scenarios:** see ### US-4.2 under Acceptance
Criteria

### US-4.3: Deactivate Orders
**As a** inventory/shipping clerk
**I want to** deactivate supplier orders
**So that** duplicate entries or cancelled orders are no longer recorded

**Priority:** P1
**Independent test:** Send a supplier order, deactivate the supplier order, check to see if the order is removed
**Acceptance scenarios:** see ### US-4.3 under Acceptance
Criteria

### US-4.4: Automatically Order Inventory When Supply Is Low
**As a** inventory/shipping clerk
**I want to** have orders automatically sent out when a product's "currentStock" is less than "minStock"
**So that** products will consistently be stocked

**Priority:** P1
**Independent test:** Change a product's "currentStock" to less than "minStock", then ensure that an order was automatically sent out
**Acceptance scenarios:** see ### US-4.4 under Acceptance
Criteria

### US-4.5: Search Supplier Orders
**As a** inventory/shipping clerk
**I want to** be able to search supplier orders using either `SupplierOrder.date` or `SupplierOrder.customerNumber`
**So that** I can easily access information about supplier orders

**Priority:** P2
**Independent test:** Inventory/shipping clerk calls `SupplierOrders.search` with the info they want to search by; supplier orders with matching information is returned
**Acceptance scenarios:** see ### US-4.6 under Acceptance
Criteria

## Requirements
### Functional Requirements
- **FR-001**: System MUST send an email within 5 minute of the order being sent
- **FR-002**: Supplier Orders MUST be sent on the specified order date at 12 am
- **FR-003**: The Supplier Order orders `Product.maxStock` - `Product.currentStock` when it is automatically sent to replenish inventory
- **FR-003**: Supplier Orders MUST not allow attribute "order" to be edited past the order date
- **FR-004**: Add a Supplier Order to `SupplierOrdersList.list` every time a Supplier Order is created
- **FR-005**: All recorded dates must be in MM/DD/YYYY format.
- **FR-006**: `orderNumber` must be incremented by one for every supplier order
- **FR-007**: Only the fields completed in the edit form are actually saved to the object
- **FR-008**: Only inventory or shipping clerks can add, edit, or deactivate a `SupplierOrder`

## Key Entities
- **SupplierOrdersList**: Contains all of the Supplier Orders ever made
- **SupplierOrder**: Contains contact info for the supplier and order details
## Data Model Requirements
### `SupplierOrdersList` table
| Field | Type | Rules |
|-------|------|-------|
| `list` | SUPPLIER_ORDER LIST | Dynamically sized |

### `SupplierOrder` table
| Field | Type | Rules |
|-------|------|-------|
| `orderName` | STRING(50) | Required |
| `orderDate` | STRING(10) | Required |
| `orderNumber` | INTEGER | Required, Auto-increment |
| `supplierOrderId` | STRING(50) | Required |
| `supplierNumber` | STRING(50) | Required |
| `email` | STRING(50) | Required |
| `poNumber` | STRING(50) | Required |
| `order` | MERCHANDISE LIST | Required, dynamically sized |
| `totalQty` | INTEGER |  Required, calculate based on `order` |
| `totalCost` | INTEGER | Required, calculate based on `order` |
| `authorizer` | STRING(20) | Required |

## Acceptance Criteria

### US-4.1 — Add Orders
#### Scenario: Order Successfully Emailed
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the clerk fills out an order form with the correct information filled out
* **Then** the email is sent with the correct information on the order date
#### Scenario: System Catches Invalid Email
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the clerk sends an order form with an invalid email
* **Then** the system responds "Enter a valid email"
#### Scenario: Date Format Incorrect
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the clerk fills out a form to add a supplier order
* **And** the date is not entered in MM/DD/YYYY format
* **Then** a `SupplierOrder` is not created
* **And** the system responds "Enter dates in MM/DD/YYYY format"

### US-4.2 — Edit Orders
#### Scenario: Order Successfully Edited
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the clerk edits an order form
* **Then** the changes are saved
* **And** the system responds "Changes Saved to [orderName]"
#### Scenario: No Changes Allowed Past Order Date
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the clerk edits an order form
* **And** it is passed the order date
* **Then** the system responds "Order date passed, can no longer edit orders"
#### Scenario: Date Entered Incorrectly
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** a clerk fills out a form to edit a supplier order
* **Then** a `SupplierOrder` is not saved
* **And** the system responds "Enter dates in MM/DD/YYYY format"

### US-4.3 — Deactivate Orders
#### Scenario: Order Successfully Deactivated
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the clerk selects and confirms a supplier order to be deactivated
* **Then** the supplier order is removed from the database

### US-4.4 — Automatically Order Inventory When Supply Is Low
#### Scenario: Restocking Order Sent
* **Given** a Product exists
* **When** a Product's `currentStock` is less than `minStock`
* **Then** an order is sent successfully
* **And** the quantity ordered is `Product.maxStock` - `Product.currentStock`

### US-4.6 — Search Supplier Orders
#### Scenario: Search Successful by Date
* **Given** an inventory clerk is logged in and authorized
* **When** the clerk searches for a supplier order within a certain time period
* **Then** the supplier orders sent during that time period appear chronologically in the search results
#### Scenario: Search Successful by Supplier Number
* **Given** an inventory clerk is logged in and authorized
* **When** the clerk searches using a supplier number
* **Then** only supply orders with that supplier number appear in search results
#### Scenario: Search Successful by Order Number
* **Given** an inventory clerk is logged in and authorized
* **When** the clerk searches using an order number
* **Then** only supply orders with that order number appear in search results
#### Scenario: No Orders In the Specified Timespan
* **Given** an inventory clerk is logged in and authorized
* **When** the clerk searches for an order order within a certain time period
* **And** there are no supplier orders in that time period
* **Then** no search results appear
#### Scenario: No Matching Supplier Numbers
* **Given** an inventory clerk is logged in and authorized
* **When** the clerk searches using a supplier number
* **And** there are no supplier orders with matching supplier numbers
* **Then** no search results appear
#### Scenario: No Matching Order Numbers
* **Given** an inventory clerk is logged in and authorized
* **When** the clerk searches using an order number
* **And** there are no supplier orders with a matching supplier number
* **Then** no search results appear