# Feature: Company Maintenance
**Feature ID:** 13
**Branch pattern:** `feature/company-maintenance`
**Status:** First Draft
**Created:** 2026-10-13
**Input:** Company managers maintain their company and subsidirary companies - add, update, deactivate
**Depends on:** [Feature 11 - User Authentication And Verification](feature-11-user-authentication-and-verification.md)[Feature 13 — Company Maintenance](feature-13-company-maintenance.md)

## User Stories

### US-13.1: Add Company
**As a** company manager
**I want to** create companies
**So that** any companies we acquire can be merged into our inventory system

**Priority:** P1
**Independent test:** A company manager creates a new `Company`
**Acceptance scenarios:** see ### US-13.1 under Acceptance
Criteria

### US-13.2: Update Company
**As a** company
**I want to** update information about a company
**So that** the company information is up to date

**Priority:** P1
**Independent test:** A company manager edits the information about a company
**Acceptance scenarios:** see ### US-13.2 under Acceptance
Criteria

### US-13.3: Deactivate Company
**As a** company
**I want to** deactivate companies from the database
**So that** formerly active companies don't clutter up the screen

**Priority:** P1
**Independent test:** A company manager deactivates an existing company
**Acceptance scenarios:** see ### US-13.3 under Acceptance
Criteria

## Requirements
### Functional Requirements
- **FR-001**: System MUST only allow a company with the  to view their own companies
- **FR-002**: Only `address`, `parentCompany`, `companyName`, and `hasParentCompany` are required to create a `Company`.
- **FR-003**: `operatingHours` must describe what days and what hours the company is open as well as any exceptions to those rules.
- **FR-004**: If `hasParentCompany` is true, `parentCompany` is true
- **FR-005**: Only a `companyManager` can edit a `Company`
- **FR-007**: Only the fields completed in the edit form are actually saved to the object
- **FR-008**: Only active objects are displayed in the UI

## Key Entities
- **Company**: A company that owns warehouses. Can be a subsidiary or parent company
## Data Model Requirements
### `users` table
| Field | Type | Rules |
|-------|------|-------|
| `companyId` | INTEGER PK | Auto-increment |
| `address` | STRING(255) | Required; follows postal service format |
| `companyDescription` | STRING(500) | Optional; contains any descriptive info about the company deemed necessary |
| `businessHours` | STRING(120) | Optional |
| `email` | STRING(120) | Optional |
| `website` | STRING(100) | Optional |
| `companyName` | STRING(100) | Required |
| `parentCompany` | COMPANY | Required if `hasParentCompany` is true |
| `hasParentCompany` | BOOLEAN | Required; Default false |
| `active` | BOOLEAN | Default true |
| `warehouses` | WAREHOUST LIST | Needs to be dynamically sized |

## Acceptance Criteria

### US-13.1 — Add Company
#### Scenario: Company Successfully Added
* **Given** a company manager has logged in and navigated to the company page
* **When** they submit the form to add company
* **And** they fill out the address, companyName, and parent company fields
* **Then** a company object is created with the correct data saved
* **And** the system responds "[Company Name] company successfully added"
#### Scenario: Not All Required Fields Filled Out
* **Given** a company manager has logged in and navigated to the company page
* **When** they submit the form to add company
* **And** they fill out the address, companyName, and parent company fields
* **Then** a company object is created
* **And** the system responds "Complete the following fields: [empty fields]"
#### Scenario: Cancel Button Clicked
* **Given** a company manager has logged in and navigated to the company page
* **When** they are filling out the form to add a company object
* **And** they click the cancel button
* **Then** the company is NOT created
* **And** the UI returns to the previous screen

### US-13.2 — Update Company
#### Scenario: Information Successfully Updated
* **Given** a company manager has logged in and navigated to the company page
* **When** they submit the form to edit a company page
* **Then** variables are updated from the fields the manager has filled out
* **And** the system responds "[Company Name] company successfully updated"
#### Scenario: Existing Warehouses Shown
* **Given** a company manager has logged in and navigated to the company page
* **When** they fill out the form to edit a company page
* **And** they are click the button to add a warehouse
* **Then** they are shown a list of active warehouses that they can choose from
#### Scenario: Warehouse Ready To Be Added
* **Given** a company manager has navigated to the company page
* **And** clicked the button to add a warehouse
* **When** they click one of the warehouses
* **Then** that warehouse appears on the searchbar as one of the warehouses to add
#### Scenario: Warehouse Addition Cancelled
* **Given** a company manager has logged in
* **And** clicked on a warehouse while filling out an edit form
* **When** they click one of the cancel button on the warehouse widget
* **Then** that warehouse is removed from the searchbar "waiting to be added" list
#### Scenario: Cancel Button Clicked
* **Given** a company manager has logged in and navigated to the company page
* **When** they are filling out the form to edit a company object
* **And** they click the cancel button to exit out of the edit form
* **Then** the company is NOT updated
* **And** the UI returns to the previous screen

### US-13.3 — Deactivate Company
#### Scenario: Employee Sucessfully Deactivated
* **Given** a company manager has logged in and navigated to the company page
* **When** they confirm that they want to deactivate a company object
* **Then** `Company.active` is changed to false
* **And** the System responds "[Company Name] company successfully deactivated"