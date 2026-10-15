# Feature: Warehouse Maintenance
**Feature ID:** 12
**Branch pattern:** `feature/warehouse-maintenance`
**Status:** First Draft
**Created:** 2026-10-13
**Input:** Companies maintain their warehouses - add, update, deactivate
**Depends on:** [Feature 11 - User Authentication And Verification](feature-11-user-authentication-and-verification.md) [Feature 13 — Company Maintenance](feature-13-company-maintenance.md)

## User Stories

### US-12.1: Add Warehouse
**As a** company manager
**I want to** create warehouses
**So that** I can have inventory systems for all of my warehouses

**Priority:** P1
**Independent test:** A company manager creates a new `Warehouse`
**Acceptance scenarios:** see ### US-12.1 under Acceptance
Criteria

### US-12.2: Update Warehouse
**As a** company manager
**I want to** update information about a warehouse
**So that** the warehouse system is up to date

**Priority:** P1
**Independent test:** A company manager edits the information about a warehouse
**Acceptance scenarios:** see ### US-12.2 under Acceptance
Criteria

### US-12.3: Deactivate Warehouse
**As a** company manager
**I want to** deactivate warehouses from the database
**So that** out of use warehouses don't clutter up the screen

**Priority:** P1
**Independent test:** A company manager deactivates an existing warehouse
**Acceptance scenarios:** see ### US-12.3 under Acceptance
Criteria

## Requirements
### Functional Requirements
- **FR-001**: System MUST only allow a company manager to view the warehouses
- **FR-002**: Only `address`, `capacity`, and `numOfAisles` are required to create a `Warehouse`.
- **FR-003**: `operatingHours` must describe what days and what hours the warehouse is open as well as any exceptions to those rules.
- **FR-007**: Only warehouse managers can add, edit, or deactivate a `Warehouse`
- **FR-007**: Only the fields completed in the edit form are actually saved to the object
- **FR-008**: Only active objects are displayed in the UI

## Key Entities
- **Warehouse**: A warehouse that the company owns
## Data Model Requirements
### `Warehouse` table
| Field | Type | Rules |
|-------|------|-------|
| `warehousId` | INTEGER PK | Auto-increment |
| `address` | STRING(255) | Required; follows postal service format |
| `warehouseDescription` | STRING(500) | Optional; contains any descriptive info about the warehouse deemed necessary |
| `managerName` | STRING(50) | Optional |
| `forkliftCount` | INTEGER | Optional |
| `capacity` | STRING(255) | Required; Describes how much/what kind of inventory the warehouse can hold |
| `numOfAisles` | INTEGER | Required |
| `operatingHours` | STRING(120) | Optional |
| `email` | STRING(120) | Optional |
| `phoneNumber` | STRING(50) | Optional |
| `active` | BOOLEAN | Default true |

## Acceptance Criteria

### US-12.1 — Add Warehouse
#### Scenario: Warehouse Successfully Added
* **Given** a company manager has logged in and navigated to the warehouse page
* **When** they submit the form to add warehouse
* **And** they fill out the address, capacity, and number of aisles fields
* **Then** a warehouse object is created
* **And** the system responds "[Warehouse Name] warehouse successfully added"
#### Scenario: Not All Required Fields Filled Out
* **Given** a company manager has logged in and navigated to the warehouse page
* **When** they submit the form to add warehouse
* **And** they fill out the address, capacity, and number of aisles fields
* **Then** a warehouse object is created
* **And** the system responds "Complete the following fields: [empty fields]"
#### Scenario: Cancel Button Clicked
* **Given** a company manager has logged in and navigated to the warehouse page
* **When** they are filling out the form to add a warehouse object
* **And** they click the cancel button
* **Then** the warehouse is NOT created
* **And** the UI returns to the previous screen

### US-12.2 — Update Warehouse
#### Scenario: Information Successfully Updated
* **Given** a company manager has logged in and navigated to the warehouse page
* **When** they submit the form to edit a warehouse page
* **Then** the warehouse is updated
* **And** the system responds "[Warehouse Name] warehouse successfully updated"
#### Scenario: Cancel Button Clicked
* **Given** a company manager has logged in and navigated to the warehouse page
* **When** they are filling out the form to edit a warehouse object
* **And** they click the cancel button
* **Then** the warehouse is NOT updated
* **And** the UI returns to the previous screen

### US-12.3 — Deactivate Warehouse
#### Scenario: Employee Sucessfully Deactivates Warehouse
* **Given** a company manager has logged in and navigated to the warehouse page
* **When** they confirm that they want to deactivate a warehouse object
* **Then** `Warehouse.active` is changed to false
* **And** the System responds "[Product Name] warehouse successfully deactivated"