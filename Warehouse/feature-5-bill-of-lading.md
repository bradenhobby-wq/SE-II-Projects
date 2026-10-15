# Feature: Bill Of Lading
**Feature ID:** 5
**Branch pattern:** `feature/bill-of-lading`
**Status:** Draft
**Created:** 2026-10-06
**Input:** Maintains bill of lading - contains dates, customer info, and the items ordered
**Depends on:** [Feature 10 — Merchandise Management](feature-10-merchandise-management.md)
**Related:** optional links to ADRs or reference docs

## User Stories
### US-5.1: Add Bill of Lading
**As a** inventory/shipping clerk
**I want to** record Bills of Lading when a shipment is received
**So that** we can check the shipment with our order

**Priority:** P1
**Independent test:** As an inventory/supplier clerk, create a Bill of Lading
**Acceptance scenarios:** see ### US-5.1 under Acceptance
Criteria

### US-5.2: Edit Bill of Lading
**As a** inventory/shipping clerk
**I want to** edit a bill of lading
**So that** we can correct any errors made during the recording

**Priority:** P1
**Independent test:** As an inventory/supplier clerk, edit a Bill of Lading, verify that the changes are saved correctly
**Acceptance scenarios:** see ### US-5.2 under Acceptance
Criteria

### US-5.3: Delete Bill of Lading
**As a** inventory/shipping clerk
**I want to** delete a bill of lading
**So that** we can keep the bills of lading updated

**Priority:** P1
**Independent test:** As an inventory/supplier clerk, delete a Bill of Lading
**Acceptance scenarios:** see ### US-5.3 under Acceptance
Criteria

### US-5.4: Search Bills of Lading
**As a** inventory/shipping clerk
**I want to** be able to search bills of lading using either `BillOfLading.date` or `BillOfLading.customerNumber`
**So that** I can easily access information about past bills of lading

**Priority:** P1
**Independent test:** Inventory/shipping clerk calls `BillOfLading.search` with the info they want to search by; bills of lading with matching information is returned
**Acceptance scenarios:** see ### US-5.4 under Acceptance
Criteria

## Requirements
### Functional Requirements
- **FR-001**: All recorded dates must be in MM/DD/YYYY format
- **FR-002**: Search results must appear within 10 seconds 99% of the time
- **FR-003**: Only warehouse or supplier clerks can manage bills of lading
- **FR-004**: The user can search by order name or by date

## Key Entities
- **Bill of Lading**: Contains all of the info in a bill of lading. Used to verify the shipment against the SupplierOrder.
## Data Model Requirements
### `BillOfLading` table
| Field | Type | Rules |
|-------|------|-------|
| `orderName` | STRING(50) | Required |
| `orderDate` | STRING(50) | Required |
| `shippedDate` | STRING(50) | Required |
| `orderNumber` | STRING(50) | Required, unique |
| `customerNumber` | STRING(50) | Required |
| `poNumber` | STRING(50) | Required |
| `orders` | MERCHANDISE LIST | Default null, dynamically sized, not required upon initialization |
| `totalQty` | INTEGER | Default 0, calculated based on `orders` |
| `totalCost` | INTEGER | Default 0, calculated based on `orders` |
| `receiverName` | STRING(50) | Required, is the name of the employee who receives the shipment |

## Acceptance Criteria

### US-5.1 — Add Bill of Lading
#### Scenario: Bill of Lading Successfully Added
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the clerk fills out a form to add a bill of lading
* **Then** a `BillOfLading` is created with the correct information
* **And** the system responds "Bill of Lading successfully created"
#### Scenario: Date Format Incorrect
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the clerk fills out a form to add a bill of lading
* **And** the date is not entered in MM/DD/YYYY format
* **Then** a `BillOfLading` is not created
* **And** the system responds "Enter dates in MM/DD/YYYY format"

### US-5.2 — Edit Bill of Lading
#### Scenario: Bill of Lading Successfully Edited
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** a clerk fills out a form to edit a bill of lading
* **Then** the changes are saved to the `BillOfLading`
* **And** the system responds "Changes saved to [`BillOfLading.orderName`]
#### Scenario: Date Entered Incorrectly
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** a clerk fills out a form to edit a bill of lading
* **Then** a `BillOfLading` is not saved
* **And** the system responds "Enter dates in MM/DD/YYYY format"

### US-5.3 — Delete Bill of Lading
#### Scenario: Bill of Lading Successfully Deleted
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the clerk selects and confirms the bill of lading to be deleted
* **Then** the bill of lading is removed from the database

### US-5.4 — Search Bills of Lading
#### Scenario: Search Successful by Date
* **Given** an inventory clerk is logged in and authorized
* **When** the clerk searches for a bill of lading within a certain time period
* **Then** the supplier orders sent during that time period appear chronologically in the search results
#### Scenario: Search Successful by Order Number
* **Given** an inventory clerk is logged in and authorized
* **When** the clerk searches using an order number
* **Then** only bills of lading with that order number appear in search results
#### Scenario: No Orders In the Specified Timespan
* **Given** an inventory clerk is logged in and authorized
* **When** the clerk searches for a bill of lading within a certain time period
* **And** there are no bills of lading in that time period
* **Then** no search results appear
#### Scenario: No Matching Supplier Numbers
* **Given** an inventory clerk is logged in and authorized
* **When** the clerk searches using an order number
* **And** there are no bills of lading with supplier numbers
* **Then** no search results appear