# Feature: Customers Management
**Feature ID:** 7
**Branch pattern:** `feature/customers-mangement`
**Status:** Draft
**Created:** 2026-10-08
**Input:** Maintain customers: add, update, delete customers
**Depends on:** [Feature 11 — User Authentication & Verification](feature-11-user-authentication-and-verification.md)

## User Stories
### US-7.1: Add Customers
**As a** shipping clerk
**I want to** be able to add customers
**So that** we can keep up with our delivery orders
**Priority:** P1
**Independent test:** Add a customer, verify the changes were saved
**Acceptance scenarios:** see ### US-7.1 under Acceptance
Criteria

### US-7.2: Edit Customers
**As a** shipping clerk
**I want to** be able to edit customers
**So that** customer information stays updated
**Priority:** P1
**Independent test:** Edit a customer, save changes, verify it saved correctly
**Acceptance scenarios:** see ### US-7.2 under Acceptance
Criteria

## US-7.3: Deactivate Customers
**As a** shipping clerk
**I want to** be able to deactivate customers
**So that** customers who no longer order from us don't clutter our search results
**Priority:** P1
**Independent test:** Deactivate a customer object, verify it doesn't appear on the search results
**Acceptance scenarios:** see ### US-7.3 under Acceptance
Criteria

## US-7.4: Search Customers
**As a** shipping clerk
**I want to** be able to search customers
**So that** I can find information about our clients easily
**Priority:** P1
**Independent test:** Search for a customer using their name or ID
**Acceptance scenarios:** see ### US-7.4 under Acceptance
Criteria

## Requirements
### Functional Requirements
- **FR-001**: System MUST only allow shipping clerks to edit, update, or deactivate customers
- **FR-002**: A name, address, email, and id is required to create a `Customer`
- **FR-003**: Only the fields completed in the edit form are actually saved to the object
- **FR-004**: The password must have at least one special character, one lower case letter, one upper case letter, and one number. It must also be 10+ characters long

## Key Entities
- **Customer**: Someone who orders shipments from the warehouse
## Data Model Requirements
### `Customer` table
| Field | Type | Rules |
|-------|------|-------|
| `address` | STRING(50) | Required |
| `name` | STRING(50) | Required |
| `email` | STRING(50) | Required |
| `id` | INTEGER PK | Required; auto-incremented |
| `password` | STRING(255) | Required; bcrypt hash only |
| `deactivated` | BOOLEAN | Default false |

## Acceptance Criteria

### US-7.1 — Add Customers
#### Scenario: Customer Successfully Created
* **Given** a shipping clerk is logged in
* **When** the clerk fills out all of the fields in the form to create a `Customer`
* **And** the clerk clicks "Save"
* **Then** a `Customer` is created
#### Scenario: Invalid Password
* **Given** a shipping clerk is logged in
* **When** the clerk fills out an invalid password in the "Create a Customer" form
* **And** the clerk clicks "Save"
* **Then** the system does not create a customer
* **And** the clerk is told the password requirements of the system
#### Scenario: Not All Fields Completed
* **Given** a shipping clerk is logged in
* **When** the clerk does NOT fill out all of the fields in the "Create a Customer" form
* **And** the clerk clicks "Save"
* **Then** the system does not create a customer
* **And** the clerk is told that they have to fill out all of the required fields
#### Scenario: Clerk Cancels Form
* **Given** a shipping clerk is logged in
* **And** the clerk has started filling out a "Create a Customer" form
* **When** the clerk clicks "Cancel"
* **Then** the UI returns to the previous screen

### US-7.2 — Edit Customers
#### Scenario: Edits Successfully Saved
* **Given** a shipping clerk has logged in and filled out a "Edit Customer" form
* **When** they click "Save"
* **Then** all changes made are saved to the `Customer` object
#### Scenario: Edits Cancelled
* **Given** a shipping clerk has logged in and started a "Edit Customer" form
* **When** they click "Cancel"
* **Then** the UI returns to the previous screen

### US-7.3 — Deactivate Customers
#### Scenario: Customer Successfully Deactivated
* **Given** a shipping clerk has logged in
* **When** they click "Deactivate" next to a `Customer` object
* **Then** `Customer.deactivated` is changed to "true"

### US-7.4 — Search Customers
#### Scenario: Relevant Search Results
* **Given** a shipping clerk has logged in
* **When** they search for a `Customer` using the "<identifier>" attribute
* **Then** the top of the search results have similar values to the search
#### Scenario: No Matching Customers
* **Given** a shipping clerk has logged in
* **When** they search for a `Customer` using the "<identifier>" attribute
* **And** no customer has a similar attribute value
* **Then** the System responds "No matching customers"

Attributes
      | identifier |
      | name       |
      | id         |
      | address    |