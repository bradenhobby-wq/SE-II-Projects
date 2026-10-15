# Feature: Customer Orders Management
**Feature ID:** 8
**Branch pattern:** `feature/customer-orders-management`
**Status:** Draft
**Created:** 2026-10-08
**Input:** Add, update, delete customer orders. Also assists in shipment to customers
**Depends on:** [Feature 7 — Customers Management](feature-7-customers-management.md)

## User Stories
### US-8.1: Customer Sends Order
**As a** customer
**I want to** order products from the warehouse
**So that** I can keep my inventory stocked

**Priority:** P1
**Independent test:** Send an order request to the warehouse, verify the data is intact
**Acceptance scenarios:** see ### US-8.1 under Acceptance
Criteria

### US-8.2: Map Out Shipping Routes
**As a** driver
**I want to** be able to see the adresses of the customers I need to visit
**So that** I can quickly deliver the products

**Priority:** P2
**Independent test:** Create multiple customer orders, have the driver view the route
**Acceptance scenarios:** see ### US-8.2 under Acceptance
Criteria

### US-8.3: Confirm Shipment Arrived
**As a** driver
**I want to** record any items that were supposed to be shipped but weren't
**So that** the customer only pays for what they received
**Priority:** P1
**Independent test:** Create customer orders, have the customer record any missing items
**Acceptance scenarios:** see ### US-8.3 under Acceptance
Criteria

### US-8.4: Search Customer Orders
**As a** shipping clerk
**I want to** search past customer orders
**So that** I can easily access past records
**Priority:** P1
**Independent test:** Create a large number of customer orders, search for specific orders
**Acceptance scenarios:** see ### US-8.4 under Acceptance
Criteria

## Requirements
### Functional Requirements
- **FR-001**: `totalQty` and `totalCost` are calculated based on `order`
- **FR-002**: Only shipping clerks can search customer orders
- **FR-003**: Only drivers can view the route
- **FR-004**: The system MUST calculate the route by calculating the shortest trip between the current location and the available stops. It recalculates this at every stop
- **FR-005**: The route MUST be displayed in order from first stop to last stop
- **FR-006**: Only the order, order date, and customer (verified via account) is required to create a `CustomerOrder` object
- **FR-007**: `fullShipmentDelivered` must change to false if missing shipment is recorded
- **FR-007**: When the driver reports missing shipments, the UI should add more fields as the driver reports missing items, allowing the driver to report as many missing items as needed
- **FR-008**: A `customerOrder` can only be searched by the `deliveryDate`, but it be a range of days
- **FR-009**: `missingShipment` is initialized to the `order` list. As the driver documents which items reached the customer, those items are removed from `missingShipment`

## Key Entities
- **Customer Route**: Displays the route the driver will use to deliver the shipment
- **Customer Order**: Contains information about the customer and order details
## Data Model Requirements
### `CustomerRoute` table
| Field | Type | Rules |
|-------|------|-------|
| `addresses` | STRING LIST | Default null |
| `route` | STRING(500) | Default "" |
### `CustomerOrder` table
| Field | Type | Rules |
|-------|------|-------|
| `orderName` | STRING(50) |
| `orderDate` | STRING(20) | Required |
| `customer` | CUSTOMER | Required |
| `order` | MERCHANDISE LIST | Required |
| `totalQty` | INTEGER | Default 0; based on `order` |
| `totalCost` | DOUBLE | Default 0; rounded to two decimal places; based on `order` |
| `authorizer` | STRING(20) |
| `deliveryDate` | STRING(20) |
| `fullShipmentDelivered` | BOOLEAN | Default true |
| `missingShipment` | MERCHANDISE LIST | 
| `totalQtyMissing` | INTEGER | Default 0; based on `missingShipment` |
| `totalCostMissing` | DOUBLE | Default 0; rounded to two decimal places; based on `missingShipment` |


## Acceptance Criteria

### US-8.1 — Customer Sends Order
#### Scenario: Customer Order Sent
* **Given** a customer has logged in and navigated to the customer order page
* **When** the customer fills out all of the required fields and clicks submit
* **Then** the order is sent to the warehouse
#### Scenario: Customer Doesn't Fill Out Required Fields
* **Given** a customer has logged in and navigated to the customer order page
* **And** the cutomer has started to fill out an order form
* **When** the customer does NOT fill out all of the required fields and clicks submit
* **Then** the system tells the user to fill out the fields
* **And** a `CustomerOrder` is not created
#### Scenario: Cancel Button Clicked
* **Given** a customer has logged in and navigated to the customer order page
* **When** the customer clicks the "Cancel" button
* **Then** the UI returns to the previous page

### US-8.2 — Map Out Shipping Routes
#### Scenario: Route Mapped Out
* **Given** a driver has logged in and navigated to the shipping route page
* **When** they fill out all of the addresses and click "Create Route"
* **Then** the addresses are sorted into the order the driver should visit them
#### Scenario: Address Doesn't Exist
* **Given** a driver has logged in and navigated to the shipping route page
* **When** they fill out all of the addresses and click "Create Route"
* **And** one of the addresses does not exist
* **Then** the system should return an error and notify the driver which address does not exist
#### Scenario: Cancel Button Clicked
* **Given** a driver has logged in and navigated to the shipping route page
* **When** the driver clicks the "Cancel" button
* **Then** the UI returns to the previous page


### US-8.3 — Confirm Shipment Arrived
#### Scenario: Driver Verifies Shipment
* **Given** a driver has logged in and navigated to the customer order page
* **When** the driver clicks on the current customer order
* **And** the driver fills out the "Missing Shipment" field and clicks "Save"
* **Then** the missing shipments are saved to `CustomerOrder` 
* **And** the system tells the driver that the results are saved
#### Scenario: Customer Doesn't Fill Out Required Fields
* **Given** a driver has logged in and navigated to the missing shipment page
* **When** the driver does NOT fill out all of the required fields and clicks submit
* **Then** the system tells the driver to fill out the fields
#### Scenario: Cancel Button Clicked
* **Given** a driver has logged in and navigated to the missing shipment page
* **When** the driver clicks the "Cancel" button
* **Then** the UI returns to the previous page

### US-8.4 — Search Customer Orders
#### Scenario: Search Results Appear
* **Given** a shipping clerk has logged in and navigated to the customer orders page 
* **When** the clerk searches for a customer order by date
* **Then** the orders in that timespan appear at the top of the search results
#### Scenario: No Orders On That Date
* **Given** a shipping clerk has logged in and navigated to the customer orders page 
* **When** the clerk searches for a customer order by date
* **And** no customer orders were delivered in that timespan
* **Then** no orders appear in the search results
* **And** the system returns a "No Results" error to the user 