# Feature: Suppliers Management
**Feature ID:** 3
**Branch pattern:** `feature/suppliers_management`
**Status:** First Draft
**Created:** 2026-10-05
**Input:** Maintain suppliers - add, update, deactivate, and search to access their information
**Depends on:** [Feature 4 — Supplier Orders Management](feature-4-suppliers-orders-management.md) [Feature 11 - User Authentication And Verification](feature-11-user-authentication-and-verification.md)

## User Stories
### US-3.1: Add suppliers
**As a** inventory clerk or shipping clerk
**I want to** be able to add suppliers
**So that** we can easily order from multiple suppliers

**Priority:** P1
**Independent test:** Inventory/shipping clerk calls `Suppliers.add` with name, ipAddress, supplierId, supplierDescription, and contactInfo; supplier appears on `SuppliersList.list`
**Acceptance scenarios:** see ### US-3.1 under Acceptance
Criteria

### US-3.2: Edit Suppliers
**As a** inventory clerk or shipping clerk
**I want to** be able to edit the suppliers
**So that** supplier's info is updated and we can easily make orders

**Priority:** P1
**Independent test:** Inventory/shipping clerk calls `Suppliers.edit` with the attributes they want to edit (function will be overloaded); updated info appears in the Supplier object
**Acceptance scenarios:** see ### US-3.2 under Acceptance
Criteria

### US-3.3: Deactivate Suppliers
**As a** inventory clerk or shipping clerk
**I want to** be able to deactivate suppliers we no longer order from
**So that** the list of suppliers isn't cluttered

**Priority:** P1
**Independent test:** Inventory/shipping clerk calls `Suppliers.deactivate` with the supplier they want to deactivate; deactivated Supplier no longer appears in the `SupplierList`
**Acceptance scenarios:** see ### US-3.3 under Acceptance
Criteria

### US-3.4: Search Suppliers
**As a** inventory clerk or shipping clerk
**I want to** be able to search suppliers by name or ID
**So that** I can easily access information about suppliers

**Priority:** P2
**Independent test:** Inventory/shipping clerk calls `Suppliers.search` with the info (name or id) they want to search by; suppliers with matching information is returned
**Acceptance scenarios:** see ### US-3.4 under Acceptance
Criteria

## Requirements
### Functional Requirements
- **FR-001**: System MUST NOT allow duplicate supplierIDs
- **FR-002**: supplierId MUST NOT increment when the suppliers are edited
- **FR-002**: System MUST NOT allow duplicate IP addresses
- **FR-003**: System MUST allow inventory clerks, shipping clerks, and management to edit, update and deactivate suppliers, but only them
- **FR-004**: Search results MUST appear before 10 seconds have passed from the search query
- **FR-005**: Search results by name pull up any suppliers with the search phrase somewhere in the name
- **FR-006**: Search results by id pull up any suppliers with the matching id
- **FR-007**: Only the fields completed in the edit form are actually saved to the object
- **FR-008**: Only active objects are displayed in the UI
- **FR-009**: Only inventory clerks and shipping clerks can add, edit, or deactivate suppliers

## Key Entities
- **SuppliersList**: Contains a list of Suppliers to display on the UI
- **Suppliers**: Contains the information necessary to recognize and contact suppliers

## Data Model Requirements
### `SuppliersList` table
| Field | Type | Rules |
|-------|------|-------|
| `list` | SUPPLIERS LIST | Required |
| `numOfSuppliers` | INTEGER | Auto-increment |

### `Suppliers` table
| Field | Type | Rules |
|-------|------|-------|
| `name` | STRING(50) | Required |
| `supplierId` | STRING(50) PK | Auto-increment |
| `ipAddress` | STRING(20) | Required, unique |
| `contactInfo` | STRING(100) | Required |
| `supplierDescription` | STRING(100) | Required |
| `orderHistory` | SUPPLIER_ORDER LIST | Not Required on Initialization, must resize to fit new objects |

## Acceptance Criteria

### US-3.1 — Add suppliers
#### Scenario: Supplier Successfully Added
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the "Add Supplier" form is filled out and submitted
* **Then** the System responds "Supplier successfully added"
* **And** the supplier and their info are now visible on the "Suppliers" page
#### Scenario: IP Address Already Taken
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the "Add Supplier" form is filled out and submitted
* **And** the IP Address in the submitted form is already recorded for another supplier
* **Then** the System responds "IP Address already being used."
* **And** the supplier and their info are now visible on the "Suppliers" page

### US-3.2 — Edit suppliers
#### Scenario: Supplier Successfully Edited
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the "Edit Supplier" form is filled out and submitted
* **Then** the System responds "Supplier successfully edited"
* **And** the supplier's updated info is now visible on the "Suppliers" page
#### Scenario: IP Address Already Taken
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the "Edit Supplier" form is filled out and submitted
* **And** the IP Address in the submitted form is already recorded for another supplier
* **Then** the System responds "IP Address already being used."
* **And** the supplier and their info are now visible on the "Suppliers" page

### US-3.3 — Deactivate suppliers
#### Scenario: Supplier Successfully Deactivated
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the clerk selects a supplier and presses the "deactivate" button
* **Then** the System responds "[supplier name] is deactivated"
* **And** that supplier is deactivated from the database

### US-3.4 — Search suppliers
#### Scenario: Verbatim Supplier Name Search Successful
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the clerk searches for a supplier using the supplier's exact name
* **Then** the supplier is the first result that pops up
#### Scenario: Similar Supplier Name Search Successful
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the clerk searches for a supplier using some of the supplier's name with slightly different cases
* **Then** the supplier is one of the first five results that pops up
#### Scenario: Invalid Supplier Name Search Returns Nothing
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the clerk searches for a supplier using a word that is in no supplier's name (like "Weird Al")
* **Then** no resuts pop up
* **And** the System responds ("no matching suppliers")
#### Scenario: Supplier ID Search Successful
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the clerk searches for a supplier using an invalid supplierId
* **Then** the supplier with that supplierId is the only result
#### Scenario: Invalid Supplier ID Search Returns Nothing
* **Given** an inventory/shipping clerk is logged in and authorized
* **When** the clerk searches for a supplier using a supplierId that isn't in use
* **Then** no results pop up

