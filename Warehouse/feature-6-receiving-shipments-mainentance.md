# Feature: Receiving Shipments Maintenance
**Feature ID:** 6
**Branch pattern:** `feature/receiving_shipments_maintenance`
**Status:** Draft
**Created:** 2026-10-07
**Input:** Maintains the receiving of shipments - both verifying that the right items were received and putting those items away
**Depends on:** [Feature 4 — supplier order maintenance](feature-4-supplier-order-maintenance.md) [Feature 5 — bill of lading maintenance](feature-5-bill-of-lading-maintenance.md) [Feature 10 — Merchandise Management](feature-10-merchandise-management.md) [Feature 11 - User Authentication And Verification](feature-11-user-authentication-and-verification.md)

## User Stories
### US-6.1: Add Received Orders
**As a** shipping clerk
**I want to** add a `ReceivedOrder`
**So that** I can keep our shipping log updated

### US-6.2: Verify Shipment
**As a** shipping clerk
**I want to** verify that the bill of lading matches the supplier order
**So that** we know if we received everything we ordered

**Priority:** P1
**Independent test:** Use the GUI to compare the BillOfLading with its matching SupplierOrder
**Acceptance scenarios:** see ### US-6.1 under Acceptance
Criteria

### US-6.3: Show Route For Putting Up Inventory
**As a** warehouse worker
**I want to** see an organized display of the locations of the items I am putting up
**So that** I can quickly navigate the warehouse when putting items away

**Priority:** P1
**Independent test:** Enter a bill of lading, click the button to see the optimized route, check that the route goes to the right place
**Acceptance scenarios:** see ### US-6.1 under Acceptance
Criteria

### US-6.4: See Missing Items
**As a** shipping clerk
**I want to** see which items were missing from the shipment, if any
**So that** I can check the reliability of suppliers

**Priority:** P1
**Independent test:** Make a `ReceivedOrder` using a matching bill of lading and supplier order, request `ReceivedOrder.missingShipment`
**Acceptance scenarios:** see ### US-6.3 under Acceptance
Criteria

### US-6.5: Edit Received Orders
**As a** shipping clerk
**I want to** edit a `ReceivedOrder`
**So that** I can fix any mistakes that were made

**Priority:** P1
**Independent test:** Make a `ReceivedOrder` using a matching bill of lading and supplier order, edit the newly created `ReceivedOrder` and save changes
**Acceptance scenarios:** see ### US-6.4 under Acceptance
Criteria

### US-6.6: Deactivate Received Orders
**As a** shipping clerk
**I want to** deactivate a `ReceivedOrders`
**So that** I can remove orders we no longer need

**Priority:** P1
**Independent test:** Make a `ReceivedOrder` using a matching bill of lading and supplier order, deactivate the newly created `ReceivedOrder`
**Acceptance scenarios:** see ### US-6.5 under Acceptance
Criteria


## Requirements
### Functional Requirements
- **FR-001**: System MUST verify that each item in `BillOfLading.orders` matches the item in `SupplierOrder.order`. Any items that do not match will be stored in `SupplierOrderStatus.missingShipment
- **FR-002**: The optimized route must be generated on creation of the `ReceivedOrder` object
- **FR-003**: `optimizedRoute` will contain a list of aisle numbers row by row with the names of items on each row
- **FR-004**: The optimized route must show the aisles closest to the receiving door first. As the user scrolls down, they see the furthest aisles
- **FR-005**: Only aisles that are being stocked with items from the shipment show up on the optimized route
- **FR-006**: Verify that `BillOfLading.orderNumber` matches `SupplierOrder.supplierOrderId` when calling `ReceivedOrder.compare` 
- **FR-007**: `receivingDoor`, `order`, and `bill` are required to create a `ReceivedOrder`
- **FR-008**: Only shipping clerks can edit, deactivate, or search received orders
- **FR-009**: When displaying the missing items, at least the unit cost, quantity, total cost, and name must be displayed for each item
- **FR-010**: Only the fields completed in the edit form are actually saved to the object
- **FR-011**: Only active objects are displayed in the UI

## Key Entities
- **ReceivedOrder**: Used to verify that all items were received on shipment and to assist warehouse worker is putting up the received shipment
## Data Model Requirements
### `ReceivedOrder` table
| Field | Type | Rules |
|-------|------|-------|
| `order` | SUPPLIER_ORDER | Required |
| `bill` | BILL_OF_LADING | Required
| `receivingDoor` | STRING(20) | Required |
| `fullShipmentReceived` | BOOLEAN | Default true |
| `missingShipment` | MERCHANDISE LIST | Dynamically sized |
| `optimizedRoute` | STRING LIST |
| `deactivated` | BOOLEAN | Default false |

## Acceptance Criteria
### US-6.1 — Add Received Orders
#### Scenario: Correct Forms Entered
* **Given** a user has filled out the form to create a `ReceivedOrder`
* **And** the `BillOfLading` and `SupplierOrder` are for the same order
* **When** the user clicks the create button
* **Then** a `ReceivedOrder` is created
#### Scenario: Forms That Don't Match Entered
* **Given** a user has filled out the form to create a `ReceivedOrder`
* **And** the `BillOfLading` and `SupplierOrder` are NOT for the same order
* **When** the user clicks the create button
* **Then** an error is thrown
#### Scenario: User Exits The Form
* **Given** a user is filling out the form to create a `ReceivedOrder`
* **When** the user clicks the cancel button
* **Then** the GUI returns to the previous screen

### US-6.2 — Verify Shipment
#### Scenario: No Missing Shipment
* **Given** a `ReceivedOrder` object has been created with a matching `BillOfLading` and `SupplierOrder`
* **And** all ordered items were shipped
* **When** the user clicks the button to view the missing shipment
* **Then** the display says that there was no missing shipment
#### Scenario: Missing Shipment Shown
* **Given** a `ReceivedOrder` object has been created with a matching `BillOfLading` and `SupplierOrder`
* **And** not all ordered items were shipped
* **When** the user clicks the button to view the missing shipment

### US-6.3 — Show Route For Putting Up Inventory
#### Scenario: Correct Route Shown Upon Request
* **Given** a warehouse worker is logged in
* **When** the worker clicks the button to show the route
* **Then** a "map" of aisles with items to stock is displayed

### US-6.4 — See Missing Items
#### Scenario: Missing Items Shown
* **Given** a shipping clerk is logged in
* **And** a `ReceivedOrder` has been created
* **And** the shipment did NOT arrive with all of the ordered items
* **When** the clerk clicks the "See Items Missing From The Shipment" button
* **Then** the UI displays all of the missing items
#### Scenario: No Missing Items
* **Given** a shipping clerk is logged in
* **And** a `ReceivedOrder` has been created
* **And** the shipment did arrive with all of the ordered items
* **When** the clerk clicks the "See Items Missing From The Shipment" button
* **Then** the system tells the user that no items were missing from the shipment

### US-6.5 — Edit Received Orders
#### Scenario: Edit Successfully Saved
* **Given** a shipping clerk is logged in
* **And** a `ReceivedOrder` object exists
* **When** the clerk edits the object and clicks "Save"
* **Then** the changes are saved to the object
* **And** the UI returns to the previous screen
#### Scenario: User Cancels Edit
* **Given** a shipping clerk is logged in
* **And** a `ReceivedOrder` object exists
* **When** the clerk starts to edit the object but clicks "Cancel"
* **Then** the changes are not saved to the object
* **And** the UI returns to the previous screen

### US-6.6 — Deactivate Received Orders
#### Scenario: Order Successfully Deactivated
* **Given** a shipping clerk is logged in
* **And** a `ReceivedOrder` object exists
* **When** the clerk clicks the "Deactivate" button by the object
* **Then** the `ReceivedOrder` is deactivated