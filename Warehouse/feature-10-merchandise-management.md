# Feature: Merchandise Management
**Feature ID:** 10
**Branch pattern:** `feature/merchandise-management`
**Status:** Draft
**Created:** 2026-10-12
**Input:** The warehouse system maintains merchandise - add, update, delete. Only the warehouse system needs to do this. Any UI created in this feature is solely meant to test that the system can receive user input to maintain merchandise.

## User Stories
### US-10.1: Add Merchandise
**As a** warehouse system
**I want to** add merchandise object on the user's request
**So that** new merchandise can be recorded

**Priority:** P1
**Independent test:** The system creates new merchandise based on user input
**Acceptance scenarios:** see ### US-10.1 under Acceptance
Criteria

### US-10.2: Update Merchandise
**As a** warehouse system
**I want to** update the merchandise attributes
**So that** the merchandise is up to date

**Priority:** P1
**Independent test:** System edits existing merchandise based on user input
**Acceptance scenarios:** see ### US-10.2 under Acceptance
Criteria

### US-10.3: Delete Merchandise
**As a** warehouse system
**I want to** delete merchandise from the database
**So that** old merchandise objects don't clutter up the database

**Priority:** P1
**Independent test:** Delete existing merchandise
**Acceptance scenarios:** see ### US-10.3 under Acceptance
Criteria

## Requirements
### Functional Requirements
- **FR-001**: System MUST receive the product id when creating `Merchandise.` This id will be used to retrieve the `Product` object
- **FR-002**: `price` and `totalPrice` must be stored rounded to two decimal places.
- **FR-003**: `totalPrice` equals `price` * `cases` * `qtyPerCase`
- **FR-004**: Only the id for the product, `price`, `cases`, and `qtyPerCase` must be passed on to initialize `Merchandise.` `price` and `product` will be initialized using the steps in FR-003 and FR-001.
- **FR-005**: During the testing phase, only a `manager` is able to create merchandise
- **FR-006**: The "merchandise" page will be deleted immediately after testing

## Key Entities
- **Merchandise**: The simplest unit of an order. It describes how many of a product is ordered at what cost.
## Data Model Requirements
### `Merchandise` table
| Field | Type | Rules |
|-------|------|-------|
| `product` | PRODUCT | Required |
| `price` | DOUBLE | Required |
| `totalPrice` | DOUBLE | Required, calculated with the formula listed in FR-003 |
| `cases` | INTEGER | Required |
| `qtyPerCase` | INTEGER | Required |

## Acceptance Criteria

### US-10.1 — Add Merchandise
#### Scenario: Merchandise Successfully Added
* **Given** a manager has logged in and navigated to the merchandise page
* **When** they submit the form to add merchandise
* **And** they fill out the  product id, price, number of cases, and quantity per case fields
* **Then** a merchandise object is created
* **And** the system responds "[Product Name] merchandise successfully added"
#### Scenario: Not All Required Fields Filled Out
* **Given** a manager has logged in and navigated to the merchandise page
* **When** they submit the form to add merchandise
* **And** they DID NOT fill out the  product id, price, number of cases, and quantity per case fields
* **Then** a merchandise object is created
* **And** the system responds "Complete the following fields: [empty fields]"
#### Scenario: Cancel Button Clicked
* **Given** a manager has logged in and navigated to the merchandise page
* **When** they are filling out the form to add a merchandise object
* **And** they click the cancel button
* **Then** the merchandise is NOT created
* **And** the UI returns to the previous screen

### US-10.2 — Update Merchandise
#### Scenario: Information Successfully Updated
* **Given** a manager has logged in and navigated to the merchandise page
* **When** they submit the form to edit a merchandise page
* **Then** the merchandise is updated
* **And** the system responds "[Product Name] merchandise successfully updated"
#### Scenario: Cancel Button Clicked
* **Given** a manager has logged in and navigated to the merchandise page
* **When** they are filling out the form to edit a merchandise object
* **And** they click the cancel button
* **Then** the merchandise is NOT updated
* **And** the UI returns to the previous screen

### US-10.3 — Delete Merchandise
#### Scenario: Employee Sucessfully Deleted
* **Given** a manager has logged in and navigated to the merchandise page
* **When** they confirm that they want to delete a merchandise object
* **Then** that merchandise is deleted from the database
* **And** the System responds "[Product Name] merchandise successfully deleted"